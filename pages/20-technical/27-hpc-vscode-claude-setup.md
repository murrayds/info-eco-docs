---
title: InfoEco Lab - HPC and VS Code Setup Guide
---

# InfoEco Lab: Getting Set Up on the UAlbany HPC

A complete, one-time setup guide for new lab members working from a Mac, off campus: VPN, SSH, Slurm, VS Code, Claude Code, and GitHub. It records what worked, what broke, and why.

- Daily routine (2 minutes): [HPC Quick Start](28-hpc-quick-start.md)
- Session length, batch tunnels, and Slurm commands: [HPC Session Routine and Time Limits](29-hpc-session-routine.md)

:::{important} The short version
1. Connect to the **GlobalProtect VPN**.
2. SSH into the head node with an **SSH key** (`ssh ualbany`).
3. Request a **compute node** with Slurm (`srun ... --propagate=NONE ...`).
4. Start a **VS Code tunnel** on that compute node (`~/code tunnel`).
5. Connect from VS Code on your Mac with the **Remote - Tunnels** extension.
6. Install **Claude Code** on the compute node and connect **git** to GitHub with an SSH key.

The usual approach (VS Code Remote-SSH) does **not** work on this cluster. See [Why Remote-SSH fails](#why-remote-ssh-fails).
:::

:::{warning} Policy check
VS Code Remote Tunnels work, but at the time of writing we had asked ITS whether they are officially permitted. Check with Prof. Murray or askIT@albany.edu for the current answer before relying on them.
:::

:::{important} Everything here is one-time
Every tool, key, and login below is saved in your home folder, which persists across sessions. After setup, each session takes about 2 minutes ([HPC Quick Start](28-hpc-quick-start.md)).
:::

---

## How the cluster is organized

Think of it as one building: **compute nodes** are the workshops where code runs (borrowed by the hour), and **storage** is the filing cabinets (permanent, visible from every node).

| Piece | Address / name | What it's for |
| --- | --- | --- |
| VPN | GlobalProtect | Required to reach the cluster from off campus |
| Head node | `head.its.albany.edu` (shows as `head-ol9`) | Logging in, managing files, git, submitting jobs. **Not** for running anything heavy |
| Compute nodes | `batch` partition, e.g. `uagc25-04` | Where all real work runs. You borrow one through Slurm |
| Home folder | `/network/rit/home/<netid>` | Your permanent storage, shared across head and compute nodes |
| Lab storage | Likely under `/network/rit/lab/` (to be confirmed) | Shared InfoEco lab folder; storage only, not a separate computer |
| JupyterLab | https://jupyterlab.its.albany.edu/ | Browser-based option, no SSH needed |

ITS documentation: *How-to: Scheduling via SLURM* and the *UAlbany Supercomputing Resources Guide* on the askIT Confluence.

---

## Step 1: VPN (GlobalProtect)

Turn on GlobalProtect from the Mac menu bar and wait for **Connected**.

:::{warning} "Connection failed, make sure the GlobalProtect service is running"
The background service wasn't running.
- System Settings → General → **Login Items & Extensions** → under **Allow in the Background**, make sure the GlobalProtect / Palo Alto Networks items are **on**.
- Check it's running: open **Activity Monitor** (Cmd+Space → "Activity Monitor") and search `PanGPS`.
- If needed, restart the services in Terminal:
  ```bash
  launchctl unload /Library/LaunchAgents/com.paloaltonetworks.gp.pangps.plist
  launchctl load /Library/LaunchAgents/com.paloaltonetworks.gp.pangps.plist
  launchctl unload /Library/LaunchAgents/com.paloaltonetworks.gp.pangpa.plist
  launchctl load /Library/LaunchAgents/com.paloaltonetworks.gp.pangpa.plist
  ```
- Restarting the Mac also fixes it often.
:::

:::{warning} "Detected another instance" popup keeps appearing
Two copies of the GlobalProtect app are running. Quit them all and let the service relaunch one:
```bash
killall GlobalProtect
```
Then use the menu bar icon to connect. Don't also open the app from Applications. Leave `PanGPS` running.
:::

:::{note} XQuartz is **not** needed for any of this.
:::

---

## Step 2: SSH nickname and SSH key (Mac → HPC)

### SSH nickname
Create `~/.ssh/config` on your Mac (`nano ~/.ssh/config`) and add:

```
Host ualbany
    HostName head.its.albany.edu
    User YOUR_NETID
```

Now `ssh ualbany` works. Seeing `head-ol9` in your prompt is normal: that's the server's own name, not your nickname.

### SSH key
Without a key, VS Code and SSH ask for your password repeatedly, and VS Code setup can time out between prompts.

```bash
ssh-keygen -t ed25519      # press Enter for all questions; if a key already exists, answer n (keep it)
ssh-copy-id ualbany        # enter your NetID password one last time
ssh ualbany                # should log in with no password
```

- `~/.ssh/id_ed25519` = private key (never share).
- `~/.ssh/id_ed25519.pub` = public key (copied to the cluster).
- `ssh-keygen` prints a fingerprint and a "randomart" box. That's just a receipt; nothing to save.

---

## Why Remote-SSH fails

This is the main trap. The standard **VS Code Remote - SSH** extension fails in two ways.

### Problem A: The head node's memory cap
VS Code shows "Downloading VS Code server" in a loop, then **"Could not fetch remote environment."** The log (View → Output → Remote - SSH) shows:

```
Fatal process out of memory: SegmentedTable::InitializeTable
```

Cause: the head node limits every process to about 500 MB of virtual memory, and the limit is locked:

```bash
ulimit -v     # 512000  (KB, about 500 MB)
ulimit -Hv    # 512000  (hard limit, so users can't raise it)
```

VS Code's server (Node.js) reserves more than that at startup and crashes immediately. Claude Code is also Node-based and hits the same wall. **This is by design:** ITS policy says no workloads on the head node.

:::{tip} Cleaning up after failed attempts
Failed connections leave a broken `~/.vscode-server` folder. On a network home folder it may refuse to delete while old processes hold files open:
```bash
pkill -u $USER -f vscode-server
rm -rf ~/.vscode-server
```
:::

### Problem B: Compute nodes block direct SSH
The usual fix is to point Remote-SSH at a compute node. On this cluster, direct SSH to compute nodes is closed, even while you have a job running there and even with an SSH key:

```bash
ssh -J ualbany NETID@uagc25-04
# Connection closed by UNKNOWN port 65535
```

So Remote-SSH can't reach the head node (memory cap) **or** the compute nodes (SSH blocked).

---

## Step 3: Get a compute node (Slurm)

From the head node (`ssh ualbany`):

```bash
srun --partition=batch --propagate=NONE --nodes=1 --time=06:00:00 --cpus-per-task=2 --mem=16G --pty $SHELL -i
```

| Flag | Meaning |
| --- | --- |
| `--partition=batch` | The general compute pool everyone can use |
| `--propagate=NONE` | **Important.** Don't copy the head node's limits (including the 500 MB cap) to the compute node |
| `--time=06:00:00` | How long you get the node (max 14 days on `batch`) |
| `--cpus-per-task=2` / `--mem=16G` | Resources requested |
| `--pty $SHELL -i` | Gives you an interactive terminal on the node |

Your prompt changes to `bash-5.1$` (the compute node's plain prompt). Check:

```bash
hostname     # e.g. uagc25-04.its.albany.edu
ulimit -v    # should say: unlimited
```

:::{warning} Closing this terminal window, or typing `exit`, ends the job and gives the node back. Your files are not affected.
:::

---

## Step 4: VS Code Remote Tunnel (the workaround)

Instead of your Mac connecting *into* the node (blocked), a small VS Code program on the node connects *out* to Microsoft's tunnel service, and your Mac connects to it through GitHub sign-in. Compute nodes have internet access (`curl -sI https://code.visualstudio.com` returns `HTTP/2 200`), so this works.

### One-time install (on the compute node)
```bash
cd ~
curl -L 'https://code.visualstudio.com/sha/download?build=stable&os=cli-alpine-x64' --output vscode_cli.tar.gz
tar -xf vscode_cli.tar.gz
```

### Start the tunnel (each session, on the compute node)
```bash
~/code tunnel --accept-server-license-terms --name ualbany-hpc
```
- First time: choose **GitHub Account**, go to https://github.com/login/device, and enter the code shown. Later runs remember the login.
- Success looks like:
  ```
  Tunnel:   ualbany-hpc
  Open:  https://vscode.dev/tunnel/ualbany-hpc
  ```
- Log lines like "Server started" and "Forwarding port" are normal. Timestamps are in UTC.
- Keep this window open while you work.

### Connect from your Mac
1. VS Code → Extensions → install **Remote - Tunnels** (Microsoft).
2. **File → New Window** (keeps any local project open), then **View → Command Palette…** → `Remote-Tunnels: Connect to Tunnel` → sign in with the **same GitHub account** → pick `ualbany-hpc`.
3. Bottom-left corner shows **Tunnel: ualbany-hpc**.
4. Verify: **Terminal → New Terminal** (or Control + `), then run `hostname`. It should be your compute node.

:::{note} On a Mac, VS Code's menus (File, View, Terminal) are in the **menu bar at the top of the screen**, not inside the window.
:::

:::{warning} "Do you want to save changes to requirements.txt?"
That's your **local** project, not the HPC: connecting in the current window closes it. Save if you edited on purpose, Don't Save if not, Cancel if unsure. Avoid it by connecting from a new window.
:::

---

## Step 5: Claude Code (on the compute node)

Install it on the **compute node**, not the head node (memory cap). It lands in your home folder, so it's a one-time install.

```bash
curl -fsSL https://claude.ai/install.sh | bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && source ~/.bashrc
claude
```

:::{warning} `bash: claude: command not found` after installing
The installer puts Claude in `~/.local/bin`, which isn't on your **PATH** (the folders the shell searches for commands). The `echo ... >> ~/.bashrc` line above adds it permanently.
:::

### Logging in
Run `claude` in the terminal, choose your Claude account, open the link in your Mac's browser, approve, and paste the code back into the terminal. A successful start shows the Claude Code banner with your plan (e.g. Claude Pro).

:::{warning} "Request failed with status code 400" when signing in from the VS Code extension
The browser redirect gets lost through the tunnel. Log in from the **terminal** instead (above); the extension then reuses that login. Afterwards run **Developer: Reload Window**.
:::

### VS Code extension
Installing **Claude Code for VS Code** (Anthropic) in the tunnel window may say: *"disabled in this workspace because it is defined to run in the Remote Extension Host."* That means it was installed on your Mac only. Open its page in the Extensions panel and click **Install in Tunnel: ualbany-hpc**.

### Tips
- Claude Code works in the folder you start it from. `cd` into your project before running `claude`.
- `claude --continue` resumes your last conversation in that folder.
- **Shift+Tab** cycles permission modes. Auto mode runs lower-risk actions without asking; while learning, a mode that asks before every change shows you what it does.

---

## Step 6: GitHub (git on the HPC)

Signing in to GitHub for the **tunnel** does not connect **git**. Git needs its own SSH key, this time created on the HPC.

```bash
ssh-keygen -t ed25519 -C "your_github_email@example.com"   # Enter for all questions
cat ~/.ssh/id_ed25519.pub                                   # copy the whole line
```

GitHub → profile picture → **Settings → SSH and GPG keys → New SSH key** → title `UAlbany HPC` → paste → **Add SSH key**.

```bash
ssh -T git@github.com
# Hi USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
git config --global user.name "Your Name"
git config --global user.email "your_github_email@example.com"
```

The "does not provide shell access" part is normal; that message means success. Clone with the **SSH** link (**Code → SSH** on the repo page): `git@github.com:OWNER/REPO.git`.

### Git and GitHub concepts

| Term | Meaning |
| --- | --- |
| Clone | Download a copy of a repo to the HPC |
| Fork | Your own copy of someone's repo on GitHub (needed only without write access) |
| Commit | A saved snapshot of changes, with a message |
| Branch | A separate line of work that doesn't touch `main` until approved |
| Push | Upload commits from the HPC to GitHub |
| Pull request (PR) | Ask the repo owner to review and merge your branch |

**If you're a collaborator on the lab repo** (you got a GitHub invite): clone → branch → commit → push → PR.
**If not:** fork on GitHub → clone your fork → branch → commit → push to your fork → PR to the lab repo.

```bash
git pull                           # get the latest first
git checkout -b my-new-feature     # new branch for this task
# ...edit files...
git add .
git commit -m "Describe what you changed"
git push -u origin my-new-feature
```
Then click **Compare & pull request** on GitHub. For your own projects: create a repo on GitHub, clone it, and push directly.

---

## Step 7: Lab storage and data

- The lab space is **storage**, not a separate computer. Code runs on a compute node and reads/writes the lab folder like any other folder.
- Find it and check access:
  ```bash
  ls /network/rit/lab/ | grep -i eco
  groups
  ```
- No folder, or "Permission denied" → ask Prof. Murray to request access from ITS.
- **Data from Google Drive:** small files can be dragged into the VS Code Explorer. Larger data: `pip install --user gdown`, then `gdown --folder "LINK"` (link shared as "Anyone with the link"), or `rclone` for very large sets. Put shared data in the lab folder if one exists; otherwise a `data/` folder in the project. Check the repo README for the expected location.

---

## What persists between sessions

| Persists (home folder) | Ends with the session |
| --- | --- |
| Claude Code install, login, and conversation history | The compute node and the tunnel |
| `~/code` tunnel program and its GitHub login | Anything still running |
| SSH keys and git config | **Unsaved** edits (press Cmd+S often) |
| Cloned projects and saved files | |

Commit and push regularly for a backup outside the cluster. Run long analyses as `sbatch` jobs ([HPC Session Routine and Time Limits](29-hpc-session-routine.md)).

---

## Fallbacks if tunnels aren't allowed

- **Terminal only:** work in the `srun` session with Claude Code in the terminal.
- **JupyterLab:** https://jupyterlab.its.albany.edu/
- **Local Mac:** clone and explore on your laptop; move to the cluster for heavy runs.

---

## Troubleshooting cheat sheet

| Symptom | Cause | Fix |
| --- | --- | --- |
| GlobalProtect "service not running" | Background service off | Login Items toggles, restart services, reboot |
| "Detected another instance" | Two GlobalProtect apps | `killall GlobalProtect` |
| Password asked over and over | No SSH key | `ssh-copy-id ualbany` |
| VS Code "Downloading server" loop / "could not fetch remote environment" | Head node 500 MB cap | Use a tunnel from a compute node, not Remote-SSH |
| `rm: Directory not empty` on `.vscode-server` | Old processes holding files | `pkill -u $USER -f vscode-server`, then `rm` again |
| `ssh uagc25-04` closes immediately | Direct SSH to compute nodes blocked | Use the tunnel |
| `ulimit -v` still 512000 on compute node | Forgot `--propagate=NONE` | Add it to `srun` |
| `claude: command not found` | `~/.local/bin` not on PATH | Add the PATH line to `~/.bashrc` |
| Claude extension "disabled in this workspace" | Installed on Mac only | **Install in Tunnel: ualbany-hpc** |
| Claude sign-in "status code 400" | Redirect lost through tunnel | Log in via `claude` in the terminal |
| `git push` asks for a password | Using HTTPS link / no key | Add HPC SSH key to GitHub; clone with the SSH link |

Help: **askIT@albany.edu** / ITS Service Desk.
