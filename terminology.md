# 专业术语

术语 | 说明
--- | ---
**macOS**        | Apple 自己的基于 UNIX 的操作系统，用于 Mac 电脑，是“让 Mac 成为 Mac 的操作系统”（"What makes a Mac a Mac"）。  
**Windows**      | Microsoft（微软）的专有操作系统，用在了很多各种各样的设备上（如果你不想头痛，保持在此系统）  
**Linux**        | 基于 Linux 内核，像 Unix 的开源操作系统家族，首个操作系统内核由 Linus Torvalds 发布于 1991 年 11 月 17 日。Linux 通常被打包进 Linux 发行版。注意，虽然 macOS 和 Linux 可能都是基于 UNIX 的，但它们有很大的不同。
**Distros（发行版）**      | 英文“Distros”是 Distributions 的缩写形式。Linux 发行版是 Linux 的分发方式。然而，当 macOS 具有发行版时，发行版就成了 macOS 安装程序和一些不是来自 Apple 的应用程序的混合。**请勿使用 macOS 发行版。**  
**Hackintosh**   | 将 macOS 安装到普通 PC 上的过程，注意，**Hackintosh 不是操作系统**，它也可以指代被经过修改而让 macOS 可以运行于其上的设备。例如：*I installed macOS on this Windows machine, therefore I have a Hackintosh. But I did NOT install "Hackintosh".（我在一台 Windows 设备上安装了 macOS，所以我进行了 Hackintosh。但是我不是安装了“Hacintosh”。）*  
**Bootloader（引导加载程序）**   | 加载操作系统的一些软件，通常由操作系统开发者创建。从技术上讲，OpenCore 本身并不是引导加载程序（查看下方对引导管理器的解释）。Apple 的 Boot.efi 其实就是在 Hackintosh 或 Mac 中的引导加载程序。
**引导管理器** | 管理引导加载程序的一些软件——我们有很多：Clover、systemd-boot、OpenCore、rEFInd、rEFIt……这些通常被看作是为真正的引导加载程序准备操作系统的软件。
---
术语 | 说明
--- | ---
**OpenCore**   | 在进行 Hackintosh 时的一个新的热门话题，由 [Acidanthera 团队](https://github.com/acidanthera)基于安全要求创建，有更快的引导速度，比 Clover 更轻量化。设置好它，需要做很多的工作，但是也支持比 Clover 更多的原生功能（例如休眠、文件保险箱 2、引导热键……）。
**Clover**  | 认为 OpenCore 发布后对经典启动支持有问题的一个引导加载程序。本指南中不会包含此软件的使用。
**ACPI**  | 高级配置与能源接口（Advanced Configuration and Power Interface，即 ACPI）为操作系统提供了一个可以发现并配置计算机硬件的开放基础，更多信息将会在此指南的剩下部分提到
**.AML** | ACPI 编译后的文件格式，你的 PC 将会执行它。`.DAT` 是另一个具有完全相同用途的扩展。
**.DSL** | ACPI 的源代码——这是你需要为你的电脑编辑并编译的文件。**不要**将这个文件格式与`.ASL`混在一起。
**Kexts（内核扩展）**   | 也称为  **K**ernel **Ext**ensions ，是 macOS 的驱动。它们用于执行不同的任务，例如用于达到不同目的的设备驱动（在 Hackintosh 中），例如修改操作系统、注入信息或执行任务。内核扩展不是优秀的 Hackintosh 的唯一部分，因为它们通常会被 ACPI 修改和修复。
**BIOS**  | 是固件用于在启动过程（上电启动）中进行硬件初始化，并为操作系统和软件提供运行时服务的基本的输入/输出系统。BIOS 固件已经预安装于一台个人电脑的主板上，是上电后首先运行的软件。（来源：维基百科）它是从上世纪 70 年代就被制造出来，且沿用至今的一部分典型软件。
**UEFI**  | Unified Extensible Firmware Interface（统一可扩展固件接口，即 UEFI）是一个在操作系统和平台固件之间规定的软件接口。UEFI 代替了在所有兼容 IBM PC 的个人电脑中现有的经典 BIOS 固件接口，并且大部分 UEFI 固件提供对经典 BIOS 服务的支持。UEFI 可以支持远程诊断和修复计算机，甚至是在没有操作系统安装的情况下。（来源：维基百科）
**UEFI 驱动** | 像其他的操作系统一样，UEFI 也有使用 Clover 或 OpenCore 加载的驱动。它们也能用于加载设备或者完成其他任务，例如使用 HfsPlus.efi 加载 Apple 的 HFS 驱动器、修正 macOS 的 `boot.efi` 等等。你可能可以在找到 `Clover 驱动` 或者 `OpenCore 驱动`，它们都是 UEFI 驱动。（注意：只有使用驱动才意味着明确了具体的引导管理器。更多信息可以在[从 Clover 转换](https://github.com/ThrRip/OpenCore-Install-Guide/tree/master/clover-conversion)页面找到）。
---
术语 | 说明
--- | ---
**EFI**   | 它有两个意思：<br/>- Mac 的固件，和 UEFI 基本相同，但是只适用于 Mac 计算机，所以不是很“普遍化”。<br/>- 在你的硬盘上用于存储让 UEFI 读取以加载操作系统的软件（例如 Windows 引导加载程序）或者 UEFI 应用程序（例如 OpenCore）的分区，它被格式化为 FAT32 并且有一个（在 16 进制中）类型为 EF00 的 ID。它可以被命名为 ESP 或 SYSTEM，并且它的大小通常是 100MB 到 400MB，但是大小并不能反映所有信息。
**MBR**   | 主引导记录（MBR） 是一种特殊类型的引导扇区，在分区的计算机大容量存储设备（如固定磁盘或可移动驱动器）的开头，用于 IBM PC 兼容系统等。 MBR 的概念在 1983 年与 PC DOS 2.0 一起公开引入。MBR 保存有关逻辑分区（包含文件系统）如何在该介质上组织的信息。MBR 还包含可执行代码，可执行代码可用作已安装的操作系统的加载器，通常通过将控制权传递到加载器的第二阶段，或与每个分区的卷启动记录 （VBR） 结合使用。此 MBR 代码通常称为引导加载程序（来源：维基百科）。此格式用于 BIOS/经典启动。MBR 格式支持最大 2TiB 和最大 4 个主分区。
**GPT**   | GUID 分区表（GPT）是物理计算机存储设备（如硬盘驱动器或固态驱动器）的分区表布局的标准，使用通用唯一标识符，也称为全局唯一标识符 （GUID）。构成统一可扩展固件接口（UEFI）标准的一部分（统一EFI论坛——对更换 PC BIOS 的建议），然而，它也用于一些BIOS系统，因为主引导记录（MBR）分区表的限制，使用 32 位逻辑块寻址（LBA）的传统 512 字节磁盘扇区（来源：维基百科）。通常，这是你要用于 UEFI 系统上的格式。 
