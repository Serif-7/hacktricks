# Physical Attacks

<details>

<summary><strong>从零开始学习AWS黑客技术，成为专家</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE（HackTricks AWS红队专家）</strong></a><strong>！</strong></summary>

支持HackTricks的其他方式：

* 如果您想看到您的**公司在HackTricks中做广告**或**下载PDF格式的HackTricks**，请查看[**订阅计划**](https://github.com/sponsors/carlospolop)!
* 获取[**官方PEASS & HackTricks周边产品**](https://peass.creator-spring.com)
* 探索[**PEASS家族**](https://opensea.io/collection/the-peass-family)，我们的独家[**NFTs**](https://opensea.io/collection/the-peass-family)
* **加入** 💬 [**Discord群**](https://discord.gg/hRep4RUj7f) 或 [**电报群**](https://t.me/peass) 或 **关注**我们的**Twitter** 🐦 [**@carlospolopm**](https://twitter.com/hacktricks\_live)**。**
* 通过向[**HackTricks**](https://github.com/carlospolop/hacktricks)和[**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) github仓库提交PR来分享您的黑客技巧。

</details>

## BIOS密码恢复和系统安全

**重置BIOS**可以通过多种方式实现。大多数主板包括一个**电池**，将其拔出约**30分钟**后，将重置BIOS设置，包括密码。另外，可以通过调整主板上的**跳线**连接特定引脚来重置这些设置。

在无法或不实际进行硬件调整的情况下，**软件工具**提供了解决方案。使用像**Kali Linux**这样的发行版从**Live CD/USB**运行系统可访问工具如_**killCmos**_和_**CmosPWD**_，可帮助恢复BIOS密码。

在BIOS密码不知道的情况下，连续**三次**输入错误密码通常会导致错误代码。此代码可用于类似[https://bios-pw.org](https://bios-pw.org)的网站，以潜在地检索可用密码。

### UEFI安全

对于使用**UEFI**而不是传统BIOS的现代系统，可以利用工具**chipsec**来分析和修改UEFI设置，包括禁用**安全启动**。可以使用以下命令完成此操作：

`python chipsec_main.py -module exploits.secure.boot.pk`

### RAM分析和冷启动攻击

RAM在断电后会短暂保留数据，通常为**1到2分钟**。通过应用液氮等冷却物质，可以将此持续时间延长至**10分钟**。在此延长期间，可以使用像**dd.exe**和**volatility**这样的工具创建**内存转储**进行分析。

### 直接内存访问（DMA）攻击

**INCEPTION**是一种通过DMA进行**物理内存操作**的工具，兼容接口如**FireWire**和**Thunderbolt**。它允许通过修补内存以接受任何密码来绕过登录程序。但是，对**Windows 10**系统无效。

### Live CD/USB用于系统访问

更改系统二进制文件如_**sethc.exe**_或_**Utilman.exe**_为_**cmd.exe**_的副本可以提供具有系统特权的命令提示符。可以使用像**chntpw**这样的工具来编辑Windows安装的**SAM**文件，从而允许更改密码。

**Kon-Boot**是一种工具，通过临时修改Windows内核或UEFI，可帮助登录Windows系统而无需知道密码。更多信息可在[https://www.raymond.cc](https://www.raymond.cc/blog/login-to-windows-administrator-and-linux-root-account-without-knowing-or-changing-current-password/)找到。

### 处理Windows安全功能

#### 启动和恢复快捷方式

* **Supr**：访问BIOS设置。
* **F8**：进入恢复模式。
* 在Windows横幅后按**Shift**可以绕过自动登录。

#### BAD USB设备

像**Rubber Ducky**和**Teensyduino**这样的设备可用作创建**恶意USB**设备的平台，能够在连接到目标计算机时执行预定义的载荷。

#### 卷影复制

管理员权限允许通过PowerShell创建敏感文件的副本，包括**SAM**文件。

### 绕过BitLocker加密

如果在内存转储文件（**MEMORY.DMP**）中找到**恢复密码**，则可能可以绕过BitLocker加密。可以利用工具如**Elcomsoft Forensic Disk Decryptor**或**Passware Kit Forensic**来实现此目的。

### 社会工程学用于添加恢复密钥

可以通过社会工程学策略添加新的BitLocker恢复密钥，说服用户执行一个添加由零组成的新恢复密钥的命令，从而简化解密过程。

<details>

<summary><strong>从零开始学习AWS黑客技术，成为专家</strong> <a href="https://training.hacktricks.xyz/courses/arte"><strong>htARTE（HackTricks AWS红队专家）</strong></a><strong>！</strong></summary>

支持HackTricks的其他方式：

* 如果您想看到您的**公司在HackTricks中做广告**或**下载PDF格式的HackTricks**，请查看[**订阅计划**](https://github.com/sponsors/carlospolop)!
* 获取[**官方PEASS & HackTricks周边产品**](https://peass.creator-spring.com)
* 探索[**PEASS家族**](https://opensea.io/collection/the-peass-family)，我们的独家[**NFTs**](https://opensea.io/collection/the-peass-family)
* **加入** 💬 [**Discord群**](https://discord.gg/hRep4RUj7f) 或 [**电报群**](https://t.me/peass) 或 **关注**我们的**Twitter** 🐦 [**@carlospolopm**](https://twitter.com/hacktricks\_live)**。**
* 通过向[**HackTricks**](https://github.com/carlospolop/hacktricks)和[**HackTricks Cloud**](https://github.com/carlospolop/hacktricks-cloud) github仓库提交PR来分享您的黑客技巧。

</details>