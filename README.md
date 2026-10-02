English | [中文](README.zh-CN.md)
# r0env2026
FinSectech reverse-engineering VM docs

An AI-assisted reverse-engineering environment for people who do not want to install Java, Frida, a proxy, and an agent from scratch.

The base system is [Omarchy](https://omarchy.org/) (Arch + Hyprland), running in VMware. You give the instructions. The agent calls tools that are already installed. The model does not replace reading assembly, and it does not guarantee that every challenge will be solved.

[![Arch](https://img.shields.io/badge/Arch-Omarchy-1793d1?logo=archlinux&logoColor=white)](https://omarchy.org/)
[![VMware](https://img.shields.io/badge/VMware-Workstation-607078)](https://www.vmware.com/)
[![arch](https://img.shields.io/badge/arch-x86__64-blue)](#extract-and-open)
[![image](https://img.shields.io/badge/image-~17GB-orange)](#download-and-verify)

The image is about 17GB and is not in this repository.

- Download page: <https://billowing-pond-8dc5.jackeyaes.workers.dev>
- Repository: <https://github.com/FinSectech-lab/r0env2026>

> [!IMPORTANT]
> Only analyze samples and challenges you are authorized to analyze. The image has no built-in API keys and does not include commercial cracking tools. Sign in to Codex and fill in your own Kimi key.

## Contents

- [What this environment is for](#what-this-environment-is-for)
- [Preinstalled](#preinstalled)
- [Download and verify](#download-and-verify)
- [Extract and open](#extract-and-open)
- [Omarchy shortcuts](#omarchy-shortcuts)
- [VM and snapshots](#vm-and-snapshots)
- [Copying files](#copying-files)
- [Proxy](#proxy)
- [Install and remove](#install-and-remove)
- [7z](#7z)
- [14-step start](#14-step-start)
- [AI tools](#ai-tools)
- [Reverse-engineering tools](#reverse-engineering-tools)
- [KCTF practice](#kctf-practice)
- [References](#references)

## What this environment is for

The usual blocker is the environment, not the challenge. Windows has no `grep`, the macOS SDK does not match, Frida and Java fight over versions, and the agent cannot connect. This VM wires the tools and the agent together first, and keeps them isolated from the host. Take a snapshot before a critical step so a failed experiment can be rolled back.

Agent entry points:

| Entry | How |
| --- | --- |
| Terminal | Type `a` |
| Shortcut | `Super + Shift + Ctrl + A` opens the default agent |
| Command | `omarchy agent prompt "Review this project"` |

Challenge attachments are on `~/Desktop`.

## Preinstalled

| Category | Tools |
| --- | --- |
| Static | jadx, apktool, radare2 |
| Dynamic | adb, Frida, r0capture |
| Traffic | tshark, Wireshark |
| Network | mihomo |
| Desktop | Firefox |
| Agent | Codex launcher, ai-memory, codebase-memory-mcp, r0crawl_skills, diagram-design, r0re, Docker |

Bring your own phone and frida-server.

## Download and verify

Put all 9 volumes in the same folder. `.001`–`.008` are `2147483648` bytes each. `.009` is `730750360` bytes.

| File | URL |
| --- | --- |
| `r0env2026.7z.001` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.001> |
| `r0env2026.7z.002` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.002> |
| `r0env2026.7z.003` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.003> |
| `r0env2026.7z.004` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.004> |
| `r0env2026.7z.005` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.005> |
| `r0env2026.7z.006` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.006> |
| `r0env2026.7z.007` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.007> |
| `r0env2026.7z.008` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.008> |
| `r0env2026.7z.009` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/r0env2026.7z.009> |
| `使用说明.txt` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/使用说明.txt> |
| `校验.txt` | <https://pub-116e2dbfb524429185afcb5d8d2c0cb1.r2.dev/校验.txt> |

Only the first volume is checked. It must equal:

```text
44690340c3e54ae98dc2ea3dde32f875
```

```bat
CertUtil -hashfile r0env2026.7z.001 MD5
```

```bash
md5sum r0env2026.7z.001
```

```bash
md5 -r r0env2026.7z.001
```

> [!WARNING]
> If it does not match, download `.001` again. Do not extract.

## Extract and open

7-Zip: <https://www.7-zip.org/download.html>

`001`–`009` must be in the same directory. Extract only `001`. The later volumes are picked up automatically.

| OS | How |
| --- | --- |
| Windows | Right-click `r0env2026.7z.001` → 7-Zip → Extract Here |
| Linux | `7z x r0env2026.7z.001` |
| macOS | Do not use Archive Utility. Use `7z x r0env2026.7z.001` |

This image is x86_64. Install VMware Workstation, open the extracted `r0env2026` folder, and double-click `其他 Linux 5.x 内核 64 位.vmx`. If asked whether the VM was moved or copied, choose **I copied it**.

| Item | Value |
| --- | --- |
| Username | `ljk` |
| Password | `123` |
| NIC | NAT |
| Suggested RAM | 8GB |

The CD drive is already set to the physical drive, so the missing Xunlei ISO warning should not appear. Challenge attachments are on `~/Desktop`.

## Omarchy shortcuts

Super is the Windows key. Windows tile and do not overlap.

| Keys | Action |
| --- | --- |
| `Super + Enter` | Terminal |
| `Super + Space` | Launcher, type to search |
| `Super + K` | Shortcut overview |
| `Super + Alt + Space` | Omarchy menu |
| `Super + Esc` | Lock, reboot, shut down |
| `Super + Shift + Enter` | Browser |
| `Super + W` | Close the current window |
| `exit` | Close the current terminal |
| `Super + Ctrl + L` | Lock screen |
| `Ctrl + Alt + Del` | Close all windows |
| `Super + C` / `Super + V` | Copy / paste |
| `Super + Ctrl + V` | Clipboard history |
| `Super + Shift + F` | File manager |
| `Super + Shift + Ctrl + A` | Default agent |

> [!NOTE]
> SSH has no graphical session. Open Firefox, Wireshark, and jadx-gui from a desktop terminal inside the VM.

## VM and snapshots

The VM runs on both Windows and macOS. Keep samples, proxy settings, and experiment config inside the VM. Snapshot before changing config, installing software, or running an unknown sample. Snapshots are in the VMware menu. Do not package and distribute the VM while it is suspended.

## Copying files

The host and the VM need to reach each other. Check the address inside the VM first:

```bash
ip -4 addr
```

NAT is usually `192.168.110.x`. From PowerShell, the password is the same as the VM login password:

```powershell
scp "C:\Users\x\Desktop\app.apk" ljk@192.168.110.134:~/Downloads/
```

A whole folder:

```powershell
scp -r "C:\Users\x\Desktop\题目" ljk@192.168.110.134:~/Downloads/
```

Confirm inside the VM:

```bash
ls ~/Downloads
```

Copy a file back to the host:

```powershell
scp ljk@192.168.110.134:~/Downloads/报告.html C:\Users\x\Desktop\
```

Use the address from `ip -4 addr`.

## Proxy

On Windows, start Clash, allow LAN, and use global mode. VM traffic goes to the host first, then out.

```bash
sudo mihomo -d ~/.config/mihomo
```

Do not close that window. The log should show `Tun adapter` and `Mixed(http+socks) proxy listening at: 127.0.0.1:7890`. In another terminal:

```bash
curl cip.cc
curl -I https://github.com
```

With TUN enabled, there is no need to `export http_proxy`. The config is `~/.config/mihomo/config.yaml`. If `nano` is missing:

```bash
sudo pacman -S --needed nano
```

Do not set the upstream to `192.168.2.1`. Under NAT the host is usually `192.168.110.1`. Change the port to match your Clash.

<details>
<summary>Minimal working config</summary>

```yaml
mixed-port: 7890
allow-lan: false
mode: rule
log-level: info

dns:
  enable: true
  listen: 0.0.0.0:1053
  enhanced-mode: fake-ip
  nameserver:
    - 8.8.8.8
    - 1.1.1.1

tun:
  enable: true
  stack: system
  auto-route: true
  auto-detect-interface: true
  strict-route: true

proxies:
  - name: HOST-CLASH
    type: socks5
    server: 192.168.110.1
    port: 1080

proxy-groups:
  - name: PROXY
    type: select
    proxies:
      - HOST-CLASH

rules:
  - IP-CIDR,127.0.0.0/8,DIRECT,no-resolve
  - IP-CIDR,10.0.0.0/8,DIRECT,no-resolve
  - IP-CIDR,172.16.0.0/12,DIRECT,no-resolve
  - IP-CIDR,192.168.0.0/16,DIRECT,no-resolve
  - MATCH,PROXY
```

</details>

Test after editing:

```bash
mihomo -t -d ~/.config/mihomo
```

Start it only after the test passes. `Ctrl+C` the old window first.

## Install and remove

Official repos:

```bash
sudo pacman -S --needed package
sudo pacman -Rns package
pacman -Ss keyword
```

AUR:

```bash
yay -S package
yay -Rns package
yay -Ss keyword
```

`sudo` does not echo the password. `--needed` skips a package that is already current. Do not prefix `yay` with `sudo`. It asks for privileges itself.

## 7z

```bash
sudo pacman -S --needed 7zip
cd ~/Downloads
7z a archive.7z directory/
7z a -tzip archive.zip directory/
7z x archive.7z -o./output
7z l archive.7z
7z t archive.7z
7z a -v2g split.7z directory/
7z x split.7z.001 -o./output
```

`a` archives, `x` extracts with paths, `l` lists, `t` tests. Do not put a space after `-o`. For split archives, extract only `.001`.

## 14-step start

1. Download the 9 volumes and the two text files.
2. Check `.001`. Extract only if it matches, and extract only `.001`.
3. Open the vmx in VMware and choose **I copied it**.
4. Boot and log in as `ljk` / `123`.
5. Run `ip -4 addr`.
6. On Windows Clash, allow LAN.
7. Write the mihomo config. Point upstream at your gateway and port.
8. Run `sudo mihomo -d ~/.config/mihomo` and leave the window open.
9. In another terminal, run `curl cip.cc` and check the exit IP.
10. Use your own ChatGPT account. Shared accounts risk bans and data leaks.
11. Run `codex` and choose Sign in with ChatGPT. Open the URL in the host browser. If the port is busy, stop the old `codex` process first.
12. Start Codex in the parent directory of the challenges and work through them with the prompts below.
13. Write each solved challenge into ai-memory, then use diagram-design for the HTML report.
14. Use `a` or `omarchy agent prompt` for system tasks such as reading logs, changing config, and checking results.

## AI tools

### codebase-memory-mcp

Builds a call graph for a repo so you do not reread the same files.

```bash
which codebase-memory-mcp
codebase-memory-mcp --help
codebase-memory-mcp install
codebase-memory-mcp --ui=true --port=9749
```

Open `http://127.0.0.1:9749`. Auto-index:

```bash
codebase-memory-mcp config set auto_index true
codebase-memory-mcp config set auto_index_limit 50000
```

To stop watching the repo in the background:

```bash
codebase-memory-mcp config set auto_watch false
```

### herdr

Shows whether the agent is working, stuck, or waiting for input.

```bash
herdr --version
herdr
herdr server stop
```

### Orca

Use this when several CLI agents need to sit side by side. It needs a display. SSH reports that none is available.

```bash
~/Applications/orca-linux.AppImage
```

### ai-memory

Keeps environment notes, evidence, and progress across sessions.

```bash
ai-memory status
```

Write a page:

```bash
ai-memory write-page --path environment.md --pinned --body '# Dev environment
- System: Omarchy (Arch + Hyprland) in VMware
- Assistant: Codex
- Long-term memory: ai-memory
'
```

A 502 means the local request was caught by the proxy:

```bash
export NO_PROXY=localhost,127.0.0.1,::1
export no_proxy=localhost,127.0.0.1,::1
grep -q 'embedding_provider' ~/.config/ai-memory/config.toml || printf '\nembedding_provider = "none"\n' >> ~/.config/ai-memory/config.toml
systemctl --user restart ai-memory.service
ai-memory status
```

Connect it to Codex:

```bash
ai-memory install-mcp --client codex --apply
ai-memory install-hooks --agent codex --apply
grep -n -i memory ~/.codex/config.toml
```

Export `NO_PROXY` again in a new terminal.

### diagram-design

In Codex, say:

```text
Use diagram-design to draw a complete reverse-engineering report
```

Open the HTML with `Super + Shift + F`. To update the plugin:

```bash
codex plugin marketplace upgrade diagram-design
```

### i-have-adhd

Write `enable adhd mode` in the prompt. The first step must be a command, and multi-step work must be numbered.

### r0crawl_skills

```bash
ls ~/.codex/skills/r0crawl_skills/SKILL.md
```

In Codex:

```text
Use r0crawl_skills. Start a beginner-friendly investigation for this target.
```

It asks for the target, the key action, the material you already have, and the result you want. For a CTF you can answer:

```text
The target is the APK in the current directory.
The action is to find a verifiable flag.
The material is this file.
Stop once the result can be reproduced.
```

### r0re

Web orchestration. Android tools run in Docker. The model is Kimi. After boot, confirm mihomo and Docker:

```bash
sudo systemctl start docker
docker images | grep cairn-android-reverse
```

Start:

```bash
cd ~/Projects/r0re
source .env
./start-r0re.sh --no-bridge --config=/home/ljk/Projects/r0re/dispatch.kimi.swarm.yaml
```

Wait for `serve ready: http://127.0.0.1:8001`. In the VM, press `Super + Shift + Enter` and open that address. Put the APK in:

```text
~/Projects/r0re/container-android/test_apk/
```

The key goes in `.env`:

```bash
KIMI_MODEL_API_KEY=your-key
```

Stop and start again after changing it. To use the host browser, open a tunnel first:

```bash
ssh -L 8001:localhost:8001 ljk@VM_IP
```

Stop:

```bash
cd ~/Projects/r0re
./start-r0re.sh --stop --no-bridge --port=8001 --config=/home/ljk/Projects/r0re/dispatch.kimi.swarm.yaml
```

## Reverse-engineering tools

They are already in the environment. The commands can be typed as-is.

**Frida**

```bash
frida --version
frida -U -f com.package.name -l hook.js
```

**jadx**

```bash
jadx --version
jadx-gui some.apk
```

**apktool**

```bash
apktool d some.apk -o ~/apktool-out
apktool b ~/apktool-out -o ~/rebuilt.apk
```

**adb**

Enable developer options and USB debugging on the phone, then attach the USB device to this VM in VMware.

```bash
adb devices
adb shell
```

If you see `unauthorized`, tap Allow on the phone.

**radare2**

```bash
r2 -v
r2 -A some.so
```

**r0capture**

Enter its own virtualenv. The system `frida` command and this tool are not the same Python:

```bash
cd ~/tools/r0capture
source .venv/bin/activate
python3 r0capture.py --help
python3 r0capture.py -U -f com.example.app -p capture.pcap
```

**Wireshark**

```bash
wireshark
```

SSH reports that no display is available. Open it from a desktop terminal, or use `tshark`.

## KCTF practice

Challenges are on `~/Desktop`. Start Codex in the parent directory:

```text
Use r0crawl_skills for every target.
The current directory contains the challenges. Analyze them one by one.
For each one, record the directory, sample, tools, evidence, and reproduction steps.
Write a finished challenge into ai-memory before starting the next one.
Stop once the result can be verified.
```

After all of them:

```text
Use diagram-design to generate a report for these challenges.
One chapter per challenge: goal, route, tools, evidence, conclusion, reproduction steps.
Add an overview at the end.
```

A prompt that names the directory, the tools, and the stop condition is less likely to spin than “just keep going.” This is a practice flow. It does not guarantee a flag for every challenge.
