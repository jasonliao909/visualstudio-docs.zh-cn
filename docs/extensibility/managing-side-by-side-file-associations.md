---
title: 管理并行文件关联|Microsoft Docs
description: 如果 VSPackage 提供文件关联，请决定如何处理并行安装，其中特定版本的 Visual Studio打开文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- verbs, setting default
ms.assetid: 9b6df3bc-d15c-4a5d-9015-948a806193b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 306643116e295342bcfb602eef370af418c87733
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664273"
---
# <a name="manage-side-by-side-file-associations"></a>管理并行文件关联

如果 VSPackage 提供文件关联，则必须决定如何处理并行安装，其中应调用特定版本的 以 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 打开文件。 不兼容的文件格式使问题进一步出现。

用户期望产品的新版本与早期版本兼容，以便可以在新版本中加载现有文件，而不会丢失数据。 理想情况下，VSPackage 可以加载和保存早期版本的文件格式。 如果事实并非如此，应提供将文件格式升级到新版本的 VSPackage。 此方法的缺点是升级后的文件无法在早期版本中打开。

若要避免此问题，可以在文件格式不兼容时更改扩展名。 例如，VSPackage 版本 1 可以使用扩展 *.mypkg10，* 版本 2 可以使用 *扩展 .mypkg20*。 此差异标识打开特定文件的 VSPackage。 如果将较新的 VSPackage 添加到与旧扩展关联的程序列表中，则用户可以右键单击该文件并选择在较新的 VSPackage 中打开该文件。 此时，VSPackage 可以提供将文件升级到新格式或打开文件并保持与早期版本的 VSPackage 的兼容性。

> [!NOTE]
> 可以组合使用这些方法。 例如，可以通过加载较旧的文件提供向后兼容性，并提供在用户保存文件格式时升级文件格式。

## <a name="face-the-problem"></a>面临问题

如果希望多个并行 VSPackage 使用相同的扩展，则必须选择与该扩展 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 关联的 版本。 下面是两种替代方法：

- 在用户计算机上安装的 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 最新版本中打开 文件。

   在此方法中，安装程序负责确定 的最新版本，并包括为文件关联编写的注册表 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 项。 在Windows安装程序包中，可以包含自定义操作以设置指示 最新版本的属性 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

  > [!NOTE]
  > 在此上下文中，"latest"表示"最新支持的版本"。 这些安装程序条目不会自动检测 的后续版本 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 "检测[系统要求](../extensibility/internals/detecting-system-requirements.md)"和"安装[](../extensibility/internals/commands-that-must-be-run-after-installation.md)后必须运行的命令"中的条目类似于此处介绍的条目，并且支持其他版本的 需要 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 这些条目。

   CustomAction 表中的以下行将 DEVENV_EXE_LATEST 属性设置为由安装后必须运行的命令中讨论的 AppSearch 和 RegLocator 表 [设置的属性](../extensibility/internals/commands-that-must-be-run-after-installation.md)。 InstallExecuteSequence 表中的行在执行序列的早期计划自定义操作。 "条件"列中的值使逻辑正常工作：

  - Visual Studio .NET 2002 是最新版本（如果它是当前的唯一版本）。

  - Visual Studio .NET 2003 是最新版本，只有当它存在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 且不存在时。

  - [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 是最新版本（如果它是唯一的当前版本）。

    最终结果是，DEVENV_EXE_LATEST包含最新版本的 devenv.exe。

  **CustomAction 表行，用于确定最新版本Visual Studio**

  |操作|类型|源|目标|
  |------------|----------|------------|------------|
  |CA_SetDevenvLatest_2002|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2002]|
  |CA_SetDevenvLatest_2003|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2003]|
  |CA_SetDevenvLatest_2005|51|DEVENV_EXE_LATEST|[DEVENV_EXE_2005]|

  **InstallExecuteSequence 表行，用于确定最新版本Visual Studio**

  |操作|条件|序列|
  |------------|---------------|--------------|
  |CA_SetDevenvLatest_2002|DEVENV_EXE_2002 和 (DEVENV_EXE_2003 或 DEVENV_EXE_2005) |410|
  |CA_SetDevenvLatest_2003|DEVENV_EXE_2003 和 not DEVENV_EXE_2005|420|
  |CA_SetDevenvLatest_2005|DEVENV_EXE_2005|430|

   可以使用 Windows Installer 包的 registry 表中的 DEVENV_EXE_LATEST 属性写入 **HKEY_CLASSES_ROOT *ProgId* ShellOpenCommand** 键的默认值 [DEVENV_EXE_LATEST] "%1"

- 运行可从可用 VSPackage 版本做出最佳选择的共享启动器程序。

   的开发人员选择了此方法来处理多种格式的解决方案和项目的复杂要求，这些格式和项目由许多 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 版本的 产生 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 在此方法中，将启动程序注册为扩展处理程序。 启动器会检查文件，并决定 的哪个版本和 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage 可以处理该特定文件。 例如，如果用户打开 VSPackage 的特定版本上次保存的文件，则启动器可以在 匹配的 版本中启动该 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] VSPackage。 此外，用户可以将启动器配置为始终启动最新版本。 启动器还可以提示用户升级文件格式。 如果文件格式包含版本号，则启动器可以通知用户文件格式是否来自高于一个或多个已安装 VSPackage 的版本。

   启动器应位于Windows版本 VSPackage 共享的应用程序安装程序组件中。 此过程确保始终安装最新版本，在卸载 VSPackage 的所有版本之前不会将其删除。 这样，即使卸载了 VSPackage 的一个版本，也保留启动器组件的文件关联和其他注册表项。

## <a name="uninstall-and-file-associations"></a>卸载和文件关联

卸载写入文件关联注册表项的 VSPackage 会删除文件关联。 因此，该扩展没有关联的程序。 Windows安装程序不会"恢复"安装 VSPackage 时添加的注册表项。 下面是修复用户文件关联的方法：

- 如前所述，使用共享启动器组件。

- 指示用户对用户想要拥有文件关联版本的 VSPackage 运行修复。

- 提供一个单独的可执行程序，用于重写相应的注册表项。

- 提供一个配置选项页或对话框，允许用户选择文件关联并回收丢失的关联。 指示用户在卸载后运行它。

## <a name="see-also"></a>另请参阅

- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)
- [为文件扩展名注册谓词](../extensibility/registering-verbs-for-file-name-extensions.md)
