---
title: VSPackages |Microsoft Docs
description: 了解 VSPackage 的常见问题以及解决问题的疑难解答提示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- VSPackages, troubleshooting
- debugging, VSPackages
ms.assetid: 274673e7-72e7-476f-a263-3411b5b874be
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a097e22bb483a638e1b02a73ff31a37261d4f5ecb99aca89dc5354ea78ece0b6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413843"
---
# <a name="troubleshooting-vspackages"></a>VSPackages 故障排除
下面是 VSPackage 的常见问题以及解决问题的提示。

### <a name="to-troubleshoot-a-vspackage-that-keeps-visual-studio-from-starting"></a>对阻止启动的 VSPackage Visual Studio进行故障排除

- 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 安全模式下启动。

   若要在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 安全模式下启动，在命令提示符下，devenv.exe **/safemode**。

   在此过程中，不会加载 VSPackage，但 包含的 VSPackage 除外 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

### <a name="to-troubleshoot-a-vspackage-that-does-not-load"></a>对不加载的 VSPackage 进行故障排除

1. 请确保使用注册 VSPackage 运行的注册表根目录，通常是实验性注册表根。

    有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

2. 如果 VSPackage 的目标是在实验性注册表根中运行，请确保正在运行 的实验版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

    若要运行实验版本，在命令窗口中键入以下内容 **：devenv /rootsuffix exp**。

3. 检查 VSPackage 注册表项。

    有关详细信息，请参阅注册[VSPackage 和管理](registering-and-unregistering-vspackages.md) [VSPackage。](../extensibility/managing-vspackages.md)

4. 打开 **无法** 加载 VSPackage 的 实例的" [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 输出"窗口。 有关 VSPackage 无法加载的原因的信息可能会显示在该窗口中。

   > [!NOTE]
   > 如果要从集成开发环境 (IDE) 启动 的实验性版本，请检查这两个版本的"输出" [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 窗口。 

5. 检查活动日志。

    有关详细信息，请参阅 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

6. 有关 IDE 引发的异常详细信息，请单击"调试"菜单上的"异常"以启用异常。 在 **"异常** "对话框中，选择想要了解详细信息的异常类型。

### <a name="to-troubleshoot-a-vspackage-that-does-not-register"></a>对未注册的 VSPackage 进行故障排除

1. 确保 VSPackage 程序集驻留在受信任的位置。 RegPkg 无法在不受信任的或部分受信任的位置（如默认 .net 安全配置中的网络共享）中注册程序集。 尽管每当用户在不受信任的位置创建项目时都会显示警告，但"不再显示此消息"复选框可以防止此警告再次出现。

### <a name="to-troubleshoot-a-command-that-is-not-visible-or-that-generates-an-error-when-you-click-a-command"></a>排查命令不可见或在单击命令时生成错误的问题

1. 在命令提示符下键入以下内容，合并新的或已更改的菜单命令以及已在 IDE 中的命令 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] **：devenv /rootsuffix Exp /setup**。

2. 请确保可以找到 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage UI.dll的组。

   1. 在注册表的"包"部分查找 VSPackage 的 CLSID：

        HKLM\Software\Microsoft\Visual Studio \\ *\<version>* \Packages

   2. 验证 SatelliteDll 子项提供的路径是否正确。

### <a name="to-troubleshoot-a-vspackage-that-behaves-unexpectedly"></a>排查出现意外行为 VSPackage 的问题

1. 在代码中设置断点。

     调试的良好起点是构造函数和初始化方法。 还可以在要评估的区域（例如菜单命令）中设置断点。 若要启用断点，必须在调试器下运行 。

    1. 在“项目”菜单上，单击“属性”   。

    2. 在" **属性页"** 对话框中，选择"调试 **"** 选项卡。

    3. 在 **"命令行参数"** 框中，键入 VSPackage 面向的开发环境的根后缀。 例如，若要选择实验性生成，请键入 **：/RootSuffix Exp**。

    4. 在" **调试"** 菜单上，单击 **"开始调试"** 或按 F5。

        > [!NOTE]
        > 如果要调试项目，现在请创建或加载项目的现有实例。

2. 使用活动日志。

     通过向活动日志写入关键点的信息来跟踪 VSPackage 行为。 在零售环境中运行 VSPackage 时，此方法特别有用。 有关详细信息，请参阅 [如何：使用活动日志](../extensibility/how-to-use-the-activity-log.md)。

3. 使用公共符号。

     若要在调试时提高可读性，可以将符号附加到调试器。

    1. 从" **工具/选项"** 菜单中，导航到 **"调试/符号"** 对话框。

    2. 将此符号 **文件 (.pdb) 位置**：

         `https://msdl.microsoft.com/download/symbols`

    3. 若要提高性能，请指定符号缓存文件夹，例如：

        ```
        C:\symbols
        ```

### <a name="to-troubleshoot-a-missing-vspackage-or-one-of-its-dependencies"></a>对缺少的 VSPackage 或其中一个依赖项进行故障排除

1. 对于托管代码，请确保引用路径正确。

   1. 在“项目”菜单上，单击“属性”   。

   2. 在"**属性页****"对话框中选择**"引用"选项卡，并确保所有路径都正确。 或者，可以使用 **对象浏览器浏览** 引用的对象。

        对于托管代码，可以使用"Fuslogvw.exe ([ 绑定日志 ](/dotnet/framework/tools/fuslogvw-exe-assembly-binding-log-viewer) 查看器") 显示失败的程序集加载的详细信息。

2. 对于非托管代码，在 CLSID 注册表节点中查找 VSPackage [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 的 CLSID：

    HKLM\Software\Microsoft\Visual Studio \\ *\<version>* \CLSID

   确保 InprocServer32 条目具有 VSPackage dll 的正确路径。

## <a name="see-also"></a>另请参阅
- [VSPackages](../extensibility/internals/vspackages.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
