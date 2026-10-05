---
title: HPC Session Routine and Time Limits
---

# HPC Session Routine and Time Limits

The details behind each work session: two ways to run the tunnel, how to pick a session length, and useful Slurm commands. For the bare checklist, see [HPC Quick Start](28-hpc-quick-start.md). For the one-time setup, see [InfoEco Lab - HPC and VS Code Setup Guide](27-hpc-vscode-claude-setup.md).

---

## Why you request time every session

The compute node is **lent** to you by Slurm for a fixed time. When the time runs out (or you `exit`), the node goes back to the shared pool and the VS Code tunnel stops.

Your **files and setup are safe**: Claude Code, the tunnel program, SSH keys, git settings, and your projects all live in your home folder, which persists. Only unsaved edits and still-running programs are lost.

:::{note} Time format
`--time=HH:MM:SS` or `--time=D-HH:MM:SS`
- `02:00:00` = 2 hours
- `08:00:00` = 8 hours
- `1-00:00:00` = 1 day
- `14-00:00:00` = 14 days, the **maximum** on the `batch` partition
:::

---

## Option A: Interactive session (simplest)

For a normal work session where you keep a Terminal window open.

**Mac Terminal:**
```bash
# 1. VPN on (GlobalProtect → Connected)
ssh ualbany

# 2. Get a compute node
srun --partition=batch --propagate=NONE --nodes=1 --time=08:00:00 --cpus-per-task=2 --mem=16G --pty $SHELL -i

# 3. Start the tunnel (leave this window open)
~/code tunnel --accept-server-license-terms --name ualbany-hpc
```

**VS Code (Mac):** File → New Window → View → Command Palette → `Remote-Tunnels: Connect to Tunnel` → `ualbany-hpc`.

**Work:** in the VS Code terminal, `cd ~/PROJECT` then `claude` (or `claude --continue`).

**When done:** save and push your work, Ctrl+C in the tunnel window, then `exit` to release the node.

:::{warning} An interactive session ends early if that Terminal window closes, Wi-Fi/VPN drops, or the Mac sleeps, no matter how much time you requested. Requesting 14 days doesn't help here. For long sessions, use Option B.
:::

---

## Option B: Batch tunnel (survives closing your laptop)

Runs the tunnel as a background job, so no Terminal window needs to stay open.

### One-time: create the script
On the head node:
```bash
nano ~/tunnel.sbatch
```
Paste:
```bash
#!/bin/bash
#SBATCH --partition=batch
#SBATCH --propagate=NONE
#SBATCH --nodes=1
#SBATCH --cpus-per-task=2
#SBATCH --mem=16G
#SBATCH --time=08:00:00
#SBATCH --job-name=vscode-tunnel
#SBATCH --output=tunnel_%j.log

~/code tunnel --accept-server-license-terms --name ualbany-hpc
```
Save: Ctrl+O, Enter, Ctrl+X.

### Each session
```bash
ssh ualbany
sbatch ~/tunnel.sbatch       # prints: Submitted batch job 123456
squeue -u $USER              # ST = R means it's running
cat ~/tunnel_123456.log      # confirm the "Tunnel: ualbany-hpc" line appears
exit                         # you can now close Terminal
```
Then connect from VS Code as usual. You can close and reopen your laptop and reconnect while the job runs.

### When done
```bash
ssh ualbany
scancel -u $USER -n vscode-tunnel
```

To change the length, edit the `#SBATCH --time=` line in `~/tunnel.sbatch`.

---

## Shortcut: one-word commands

On the head node, add aliases to `~/.bashrc` once:
```bash
echo "alias getnode='srun --partition=batch --propagate=NONE --nodes=1 --time=08:00:00 --cpus-per-task=2 --mem=16G --pty \$SHELL -i'" >> ~/.bashrc
echo "alias tunnel='~/code tunnel --accept-server-license-terms --name ualbany-hpc'" >> ~/.bashrc
source ~/.bashrc
```
Now each session is `ssh ualbany` → `getnode` → `tunnel`. Change the default time by editing the `getnode` line in `~/.bashrc`.

---

## Choosing a time limit

| Use case | Suggested `--time` |
| --- | --- |
| Quick test | `01:00:00` to `02:00:00` |
| An evening of work | `04:00:00` to `08:00:00` |
| Full day | `12:00:00` or `1-00:00:00` (use Option B) |
| Long-running analysis | A regular `sbatch` job for the analysis itself, up to `14-00:00:00` |

:::{tip} Why not always request the maximum (14 days)?
- Longer and bigger requests can **wait longer in the queue**.
- The node is **reserved the whole time**, even while you sleep, which takes resources from others on a shared cluster.
- Exceptions beyond 14 days or 3 nodes: email askIT@albany.edu.

Request about as long as you'll actually work, and cancel early when done.
:::

---

## Useful commands

| Command | What it does |
| --- | --- |
| `squeue -u $USER` | Your running and waiting jobs |
| `scontrol show job JOBID` | Details of a job, including `EndTime` |
| `scancel JOBID` | Cancel a job |
| `sinfo -p batch` | How busy the batch partition is |
| `hostname` | Which machine you're on |
| `ulimit -v` | Memory cap (`unlimited` on a compute node with `--propagate=NONE`) |
| `claude --continue` | Resume your last Claude Code conversation in this folder |
