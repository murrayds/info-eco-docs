---
title: HPC Quick Start
---

# HPC Quick Start (about 2 minutes)

Setup is done. Just do this each session. Details: [HPC Session Routine and Time Limits](29-hpc-session-routine.md) · Full setup and fixes: [InfoEco Lab - HPC and VS Code Setup Guide](27-hpc-vscode-claude-setup.md)

## Start

1. **VPN:** GlobalProtect (menu bar) → **Connected**
2. **Mac Terminal:**
   ```bash
   ssh ualbany
   ```
3. **Get a compute node** (change `08:00:00` to the hours you need; max `14-00:00:00`):
   ```bash
   srun --partition=batch --propagate=NONE --nodes=1 --time=08:00:00 --cpus-per-task=2 --mem=16G --pty $SHELL -i
   ```
4. **Start the tunnel** (leave this window open):
   ```bash
   ~/code tunnel --accept-server-license-terms --name ualbany-hpc
   ```
5. **VS Code:** File → New Window → View → Command Palette → `Remote-Tunnels: Connect to Tunnel` → **ualbany-hpc**
   Check the bottom-left says **Tunnel: ualbany-hpc**.

## Work

In the VS Code terminal (Control + `):
```bash
cd ~/PROJECT_NAME
git pull                     # get the latest
claude --continue            # or just: claude
```
Save often with **Cmd+S**.

## Finish

```bash
git add .
git commit -m "What I changed"
git push
```
Then **Ctrl+C** in the tunnel window → `exit` (gives the node back).

## If something's off

| Problem | Quick fix |
| --- | --- |
| Can't connect at all | Is the VPN on? |
| `srun` waits a long time | Ask for less time or memory |
| VS Code can't find `ualbany-hpc` | Is the tunnel window still open? Did the session time run out? |
| Prompt shows `head-ol9`, not `bash-5.1$` | You're not on a compute node yet; run step 3 |
| Session ended unexpectedly | Your files are safe; repeat steps 3 to 5 |

:::{tip} Check how much time is left: `squeue -u $USER` (TIME = time used; TIME_LIMIT shown with `scontrol show job JOBID`).
:::
