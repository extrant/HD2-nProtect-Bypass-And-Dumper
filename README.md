# HD2-nProtect-Bypass-And-Dumper

[中文版本](#中文版本) | [English Version](#english-version)

---

安全报告 | Safety Report

安恒云沙箱：https://sandbox.dbappsecurity.com.cn/report/04d0311a-3a22-462c-9f4b-d6550f01acb6

virustotal：https://www.virustotal.com/gui/file/f76a753be609a7c81792088dac753ddfcfd7ef5073269905073c1cccdda15472/detection

TX：https://tix.qq.com/search/single?keyword=c48a168f46444c0841ff3fd8e551e25a

---
## 中文版本

### 项目简介
HD2 Siren Toolkit 是一款专为 *Helldivers 2* 开发的轻量级底层调试与逆向工具。该项目使用 C# 原生开发，旨在通过内核级驱动绕过 GameGuard (GG) 保护，并提供解密后的游戏模块导出（Dump）功能，以便于进行离线分析。

### 核心功能
*   **GG 保护绕过 (Bypass)**：严格遵循 Phase 1/2/3 逻辑，自动应用内存补丁并清理监控进程。
*   **模块导出 (Module Dump)**：支持将内存中活跃的 `game.dll` 和 `helldivers2.exe` 导出为磁盘 PE 文件。
*   **内核驱动支持**：内置驱动加载器，通过内核级权限访问受保护进程。
*   **自动化流程**：自动处理管理员提权、进程查找、窗口监控以及 10 秒的联网稳定性等待（支持按 'K' 跳过）。

### 使用说明
1.  **准备环境**：确保程序目录下存在 `pe_unmapper.exe`。
2.  **启动程序**：以管理员身份运行 `HD2Hacks.exe`。
3.  **启动游戏**：在游戏启动或进入主界面时，观察工具控制台。
4.  **执行操作**：
    *   程序会检测到 `helldivers2.exe` 进程及窗口。
    *   Bypass 应用成功后，你会看到绿色渐变的 **SIREN** 标志。
    *   在菜单中选择 `[1]` 导出 DLL，或选择 `[2]` 导出 EXE。

### 注意事项
*   本工具仅供学习与逆向工程研究使用。
*   由于涉及驱动加载，杀毒软件可能会误报，请自行排除。
*   十分建议在进入飞船后再启动这个绕过脚本。由于为了防止被箭头发现具体实现，对本体进行了混淆，但我保证代码绝对是安全的。

---

## English Version

### Introduction
HD2 Siren Toolkit is a lightweight, low-level debugging and reverse engineering tool designed for *Helldivers 2*. Developed natively in C#, this project focuses on bypassing GameGuard (GG) protection via a kernel-mode driver and providing decrypted module dumping for offline analysis (IDA/x64dbg).

### Core Features
*   **GameGuard Bypass**: Strictly follows the Phase 1/2/3 logic to apply memory patches and terminate monitoring processes.
*   **Module Dumping**: Export live `game.dll` and `helldivers2.exe` from memory into standard PE files.
*   **Kernel Driver Support**: Integrated driver loader to handle protected process access via `NyNyDrv.sys`.
*   **Automated Workflow**: Handles UAC elevation, process scanning, window monitoring, and a 10s stability delay (skippable via 'K').

### How to Use
1.  **Preparation**: Ensure `pe_unmapper.exe` is in the same directory as the executable.
2.  **Launch**: Run `HD2Hacks.exe` as Administrator.
3.  **Start Game**: Launch the game and wait for the tool to detect the process.
4.  **Execute**:
    *   The tool will wait for the `helldivers2.exe` process and its main window.
    *   Once the **SIREN** banner appears in green, the bypass is active.
    *   Use the menu to export modules: `[1]` for DLL, `[2]` for EXE.

### Disclaimer
*   This tool is for educational purposes and reverse engineering research only.
*   As it involves kernel driver loading, security software may flag it as a threat. Use at your own risk.
*   It is highly recommended to initialize the bypass script only after you have successfully boarded the spacecraft. To protect the core implementation logic from detection by Arrowhead, the binary has been obfuscated. I can personally guarantee that the code is entirely safe and contains no malicious components.
---

### Technical Sequence
```text
Phase 1: Apply P1-P8 Memory Patches (Strip protection)
Phase 2: Force Terminate GameMon.des (Process cleanup)
Phase 3: Silence Engine Logger (Heartbeat suppression)
```

**Author**: Siren  
**Built for Liberty.**
