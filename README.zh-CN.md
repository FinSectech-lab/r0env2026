[English](README.md) | 中文
# r0env2026

AI 自动化逆向环境。给不想从零装 Java、Frida、代理和 Agent 的人。

底层是 [Omarchy](https://omarchy.org/)（Arch + Hyprland），跑在 VMware 里。人下指令，Agent 调已经装好的工具。模型不代替读汇编，也不保证解出所有题。

[![Arch](https://img.shields.io/badge/Arch-Omarchy-1793d1?logo=archlinux&logoColor=white)](https://omarchy.org/)
[![VMware](https://img.shields.io/badge/VMware-Workstation-607078)](https://www.vmware.com/)
[![arch](https://img.shields.io/badge/arch-x86__64-blue)](#解压与打开)
[![image](https://img.shields.io/badge/image-~17GB-orange)](#下载与校验)

镜像约 17GB，不在本仓库。

- 下载页：<https://billowing-pond-8dc5.jackeyaes.workers.dev>
- 仓库：<https://github.com/FinSectech-lab/r0env2026>

> [!IMPORTANT]
> 只分析自己有权分析的样本和题目。镜像里没有现成密钥，不含商业破解工具。Codex 和 Kimi 要自己登录或填写密钥。

## 目录

- [这套环境解决什么](#这套环境解决什么)
- [已预装](#已预装)
- [下载与校验](#下载与校验)
- [解压与打开](#解压与打开)
- [Omarchy 快捷键](#omarchy-快捷键)
- [虚拟机与快照](#虚拟机与快照)
- [传文件](#传文件)
- [代理](#代理)
- [安装与卸载](#安装与卸载)
- [7z](#7z)
- [14 步上手](#14-步上手)
- [AI 工具](#ai-工具)
- [逆向工具](#逆向工具)
- [KCTF 练习](#kctf-练习)
- [参考](#参考)

## 这套环境解决什么

常见卡点是环境，不是题目本身。Windows 没有 `grep`，macOS SDK 对不上，Frida 和 Java 版本打架，Agent 又连不上。这台虚拟机把工具和 Agent 先接好，和主机隔离。关键步骤前可以打快照，试错后能退回去。

Agent 入口：

| 入口 | 用法 |
| --- | --- |
| 终端 | 输入 `a` |
| 快捷键 | `Super + Shift + Ctrl + A` 打开默认 Agent |
| 命令 | `omarchy agent prompt "Review this project"` |

题目附件在 `~/Desktop`。

## 已预装

| 类别 | 工具 |
| --- | --- |
| 静态 | jadx、apktool、radare2 |
| 动态 | adb、Frida、r0capture |
| 流量 | tshark、Wireshark |
| 网络 | mihomo |
| 桌面 | Firefox |
| Agent | Codex 启动器、ai-memory、codebase-memory-mcp、r0crawl_skills、diagram-design、r0re、Docker |

手机和 frida-server 自备。

## 下载与校验

9 个分卷放同一文件夹。`.001`–`.008` 各 `2147483648` 字节，`.009` 为 `730750360` 字节。

| 文件 | 地址 |
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

只校验第一卷。必须等于：

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
> 对不上就重新下载 `.001`，不要解压。

## 解压与打开

7-Zip：<https://www.7-zip.org/download.html>

`001`–`009` 必须在同一目录。只解压 `001`，后面的分卷会自动接上。

| 系统 | 做法 |
| --- | --- |
| Windows | 右键 `r0env2026.7z.001` → 7-Zip → 解压到当前目录 |
| Linux | `7z x r0env2026.7z.001` |
| macOS | 不要用归档实用工具，用 `7z x r0env2026.7z.001` |

本镜像为 x86_64。安装 VMware Workstation，打开解压出的 `r0env2026`，双击「其他 Linux 5.x 内核 64 位.vmx」。询问已移动或已复制时，选「我已复制此虚拟机」。

| 项 | 值 |
| --- | --- |
| 用户名 | `ljk` |
| 密码 | `123` |
| 网卡 | NAT |
| 内存建议 | 8GB |

光驱已设为物理驱动器，不应再报迅雷 ISO 缺失。题目附件在 `~/Desktop`。

## Omarchy 快捷键

Super 是 Windows 键。窗口平铺，不重叠。

| 按键 | 作用 |
| --- | --- |
| `Super + Enter` | 终端 |
| `Super + Space` | 启动器，打字搜程序 |
| `Super + K` | 快捷键一览 |
| `Super + Alt + Space` | Omarchy 菜单 |
| `Super + Esc` | 锁屏、重启、关机 |
| `Super + Shift + Enter` | 浏览器 |
| `Super + W` | 关闭当前窗口 |
| `exit` | 关闭当前终端 |
| `Super + Ctrl + L` | 锁屏 |
| `Ctrl + Alt + Del` | 关闭所有窗口 |
| `Super + C` / `Super + V` | 复制 / 粘贴 |
| `Super + Ctrl + V` | 剪贴板历史 |
| `Super + Shift + F` | 文件管理器 |
| `Super + Shift + Ctrl + A` | 默认 Agent |

> [!NOTE]
> SSH 里没有图形界面。Firefox、Wireshark、jadx-gui 要在虚拟机桌面终端开。

## 虚拟机与快照

Windows 和 macOS 都能跑这台虚拟机。样本、代理和实验配置留在虚拟机里。改配置、装软件、跑未知样本之前，先打快照。快照在 VMware 菜单里，不要在虚拟机还挂起时打包分发。

## 传文件

主机和虚拟机要能互通。虚拟机里先看地址：

```bash
ip -4 addr
```

NAT 常见 `192.168.110.x`。PowerShell 把文件传进去，密码与虚拟机登录密码相同：

```powershell
scp "C:\Users\x\Desktop\app.apk" ljk@192.168.110.134:~/Downloads/
```

整夹：

```powershell
scp -r "C:\Users\x\Desktop\题目" ljk@192.168.110.134:~/Downloads/
```

虚拟机里确认：

```bash
ls ~/Downloads
```

从虚拟机拷回主机：

```powershell
scp ljk@192.168.110.134:~/Downloads/报告.html C:\Users\x\Desktop\
```

IP 以 `ip -4 addr` 为准。

## 代理

Windows 上开 Clash，允许局域网，走全局。虚拟机流量先到宿主机，再出去。

```bash
sudo mihomo -d ~/.config/mihomo
```

窗口不要关。日志里应有 `Tun adapter` 和 `Mixed(http+socks) proxy listening at: 127.0.0.1:7890`。另开终端：

```bash
curl cip.cc
curl -I https://github.com
```

开着 TUN 不必再 `export http_proxy`。配置在 `~/.config/mihomo/config.yaml`。没有 nano 时用：

```bash
sudo pacman -S --needed nano
```

上游不要写 `192.168.2.1`。NAT 下宿主机一般是 `192.168.110.1`，端口按自己的 Clash 改。

<details>
<summary>最小可用配置</summary>

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

改完先测：

```bash
mihomo -t -d ~/.config/mihomo
```

通过后再启动。旧窗口先 `Ctrl+C`。

## 安装与卸载

官方源：

```bash
sudo pacman -S --needed 软件名
sudo pacman -Rns 软件名
pacman -Ss 关键词
```

AUR：

```bash
yay -S 软件名
yay -Rns 软件名
yay -Ss 关键词
```

`sudo` 输入密码时不显示字符。`--needed` 表示已是当前版本就跳过。`yay` 前面不用加 `sudo`，需要权限时它自己问。

## 7z

```bash
sudo pacman -S --needed 7zip
cd ~/Downloads
7z a 压缩包.7z 目录名/
7z a -tzip 压缩包.zip 目录名/
7z x 压缩包.7z -o./输出目录
7z l 压缩包.7z
7z t 压缩包.7z
7z a -v2g 分卷.7z 目录名/
7z x 分卷.7z.001 -o./输出目录
```

`a` 压缩，`x` 按目录解压，`l` 只列出，`t` 测试。`-o` 后面不加空格。分卷只解压 `.001`。

## 14 步上手

1. 下载 9 个分卷和两份说明。
2. 校验 `.001`。对得上再解压，只解压 `.001`。
3. VMware 打开 vmx，选「我已复制此虚拟机」。
4. 开机，登录 `ljk` / `123`。
5. `ip -4 addr` 看地址。
6. Windows Clash 允许局域网。
7. 写 mihomo 配置，上游改成自己的网关和端口。
8. `sudo mihomo -d ~/.config/mihomo`，窗口别关。
9. 另开终端，`curl cip.cc` 看出口。
10. 用自己的 ChatGPT 账号。共享号有封号和资料泄露风险。
11. 终端输入 `codex`，选 Sign in with ChatGPT。把给出的网址在主机浏览器打开。端口占用时先关掉旧的 `codex` 进程。
12. 在题目父目录启动 Codex，按下面的练习提示词逐题做。
13. 一题一题写入 ai-memory，最后用 diagram-design 出 HTML。
14. `a` 或 `omarchy agent prompt` 处理系统任务，例如看日志、改配置、复核结果。

## AI 工具

### codebase-memory-mcp

给仓库建调用图，少反复读文件。

```bash
which codebase-memory-mcp
codebase-memory-mcp --help
codebase-memory-mcp install
codebase-memory-mcp --ui=true --port=9749
```

浏览器打开 `http://127.0.0.1:9749`。自动索引：

```bash
codebase-memory-mcp config set auto_index true
codebase-memory-mcp config set auto_index_limit 50000
```

不想后台盯着仓库：

```bash
codebase-memory-mcp config set auto_watch false
```

### herdr

看 Agent 在干活、卡住，还是在等输入。

```bash
herdr --version
herdr
herdr server stop
```

### Orca

多个 CLI Agent 并排时再用。需要图形界面，SSH 里会报没有 display。

```bash
~/Applications/orca-linux.AppImage
```

### ai-memory

跨会话记环境、证据和进度。

```bash
ai-memory status
```

写入一条：

```bash
ai-memory write-page --path environment.md --pinned --body '# 开发环境
- 系统：VMware 里的 Omarchy（Arch + Hyprland）
- 助手：Codex
- 长期记忆：ai-memory
'
```

502 时，本机请求被代理拦住：

```bash
export NO_PROXY=localhost,127.0.0.1,::1
export no_proxy=localhost,127.0.0.1,::1
grep -q 'embedding_provider' ~/.config/ai-memory/config.toml || printf '\nembedding_provider = "none"\n' >> ~/.config/ai-memory/config.toml
systemctl --user restart ai-memory.service
ai-memory status
```

接入 Codex：

```bash
ai-memory install-mcp --client codex --apply
ai-memory install-hooks --agent codex --apply
grep -n -i memory ~/.codex/config.toml
```

新终端要再 export 一次 `NO_PROXY`。

### diagram-design

在 Codex 里说：

```text
用 diagram-design 画完整逆向报告
```

HTML 用 `Super + Shift + F` 打开。要更新插件：

```bash
codex plugin marketplace upgrade diagram-design
```

### i-have-adhd

提示词里写「开启 adhd mode」。要求第一步先给命令，多步要编号。

### r0crawl_skills

```bash
ls ~/.codex/skills/r0crawl_skills/SKILL.md
```

Codex 里：

```text
Use r0crawl_skills. Start a beginner-friendly investigation for this target.
```

它会问分析对象、关键动作、已有材料、要什么结果。CTF 可以回：

```text
目标是当前目录的 APK。
动作是找到可验证的 flag。
材料就是这个文件。
找到可复现结果再停。
```

### r0re

网页编排。Docker 里跑 Android 工具，模型走 Kimi。开机后先确认 mihomo 和 Docker：

```bash
sudo systemctl start docker
docker images | grep cairn-android-reverse
```

启动：

```bash
cd ~/Projects/r0re
source .env
./start-r0re.sh --no-bridge --config=/home/ljk/Projects/r0re/dispatch.kimi.swarm.yaml
```

看到 `serve ready: http://127.0.0.1:8001`。虚拟机里 `Super + Shift + Enter` 打开浏览器，访问这个地址。APK 放到：

```text
~/Projects/r0re/container-android/test_apk/
```

Key 写在 `.env`：

```bash
KIMI_MODEL_API_KEY=你的密钥
```

改完要停掉再启动。主机浏览器要先建隧道：

```bash
ssh -L 8001:localhost:8001 ljk@虚拟机IP
```

停止：

```bash
cd ~/Projects/r0re
./start-r0re.sh --stop --no-bridge --port=8001 --config=/home/ljk/Projects/r0re/dispatch.kimi.swarm.yaml
```

## 逆向工具

都在环境里，命令可直接打。

**Frida**

```bash
frida --version
frida -U -f com.包名 -l hook.js
```

**jadx**

```bash
jadx --version
jadx-gui 某.apk
```

**apktool**

```bash
apktool d 某.apk -o ~/apktool-out
apktool b ~/apktool-out -o ~/rebuilt.apk
```

**adb**

手机开开发者选项和 USB 调试，VMware 把 USB 勾给这台虚拟机。

```bash
adb devices
adb shell
```

出现 `unauthorized` 时，在手机上点允许。

**radare2**

```bash
r2 -v
r2 -A 某.so
```

**r0capture**

要进它自己的虚拟环境。系统里的 `frida` 命令和这里不是同一套 Python：

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

SSH 里会报没有 display。桌面终端开，或只用 `tshark`。

## KCTF 练习

题目在 `~/Desktop`。在父目录开 Codex：

```text
Use r0crawl_skills for every target.
当前目录包含题目，请逐题分析。
每题记录目录、样本、工具、证据和复现步骤。
完成一题写入 ai-memory，再做下一题。
找到可验证结果再停。
```

全部完成后再说：

```text
用 diagram-design 为这些题生成报告。
每题一章：目标、路线、工具、证据、结论、复现步骤。
最后加总览。
```

提示词写清目录、工具和停机条件，比只说「一直跑」更不容易空转。
