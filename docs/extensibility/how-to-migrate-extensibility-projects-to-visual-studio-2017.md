---
title: 将扩展性项目迁移到 Visual Studio 2017
titleSuffix: ''
description: 了解如何将扩展性项目升级到 Visual Studio 2017，以及如何从扩展清单版本 2 升级到版本 3 VSIX 清单。
ms.custom: SEO-VS-2020
ms.date: 11/09/2016
ms.topic: how-to
ms.assetid: 8ca07b00-a3ff-40ab-b647-c0a93b55e86a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 9e10a9061eae777728b9874c959483edfc7abe15
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050333"
---
# <a name="how-to-migrate-extensibility-projects-to-visual-studio-2017"></a>如何：将扩展性项目迁移到 Visual Studio 2017

本文档介绍如何将扩展性项目升级到 Visual Studio 2017。 除了介绍如何更新项目文件外，还介绍了如何从扩展清单版本 2 (VSIX v2) 升级到新版本 3 VSIX 清单格式 (VSIX v3) 。

## <a name="install-visual-studio-2017-with-required-workloads"></a>安装Visual Studio工作负载的 2017 年 1 月

请确保安装包括以下工作负载：

* .NET 桌面开发
* Visual Studio 扩展开发

## <a name="open-vsix-solution-in-visual-studio-2017"></a>在 2017 Visual Studio打开 VSIX 解决方案

所有 VSIX 项目都需要从主版本单向升级到 2017 Visual Studio版本。

项目文件 (例如 **.csproj*) 将更新：

* MinimumVisualStudioVersion - 现在设置为 15.0
* OldToolsVersion (（如果以前存在) - 现在设置为 14.0

## <a name="update-the-microsoftvssdkbuildtools-nuget-package"></a>更新 Microsoft.VSSDK.BuildTools NuGet包

> [!Note]
> 如果解决方案未引用 Microsoft.VSSDK.BuildTools NuGet包，可以跳过此步骤。

若要以新的 VSIX v3 (版本 3) 格式生成扩展，需要使用新的 VSSDK 生成工具生成解决方案。 这将随 2017 Visual Studio一起安装，但 VSIX v2 扩展可能通过 NuGet。 如果是这样，则需要为解决方案手动安装 Microsoft.VSSDK.BuildTools NuGet包的更新。

若要更新NuGet Microsoft.VSSDK.BuildTools 的引用：

* 右键单击解决方案，然后选择"**管理解决方案NuGet包"。**
* 导航到"更新 **"** 选项卡。
* 选择 **"Microsoft.VSSDK.BuildTools (最新版本) "。**
* 按 **"更新"。**

![VSSDK 生成工具](media/vssdk-build-tools.png)

## <a name="make-changes-to-the-vsix-extension-manifest"></a>对 VSIX 扩展清单进行更改

若要确保用户安装 Visual Studio具有运行扩展所需的所有程序集，请指定扩展清单文件中的所有必备组件或包。 当用户尝试安装扩展时，VSIXInstaller 将检查是否安装了所有必备组件。 如果缺少某些组件，系统会在扩展安装过程中提示用户安装缺少的组件。

> [!Note]
> 所有扩展至少应指定Visual Studio编辑器组件作为先决条件。

* 编辑扩展清单文件 (通常称为 *source.extension.vsixmanifest) 。*
* 确保 `InstallationTarget` 包含 15.0。
* 添加所需的安装 (，如以下示例所示) 。
  * 建议仅为安装先决条件指定组件 ID。
  * 有关标识组件标识的说明，请参阅本文档末尾 [的 部分](#find-component-ids)。

示例：

```xml
<PackageManifest>
 ...
    <Prerequisites>
        <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Component.DiagnosticTools" Version="[15.0.25814.0,16.0)" />
        <Prerequisite Id="Microsoft.VisualStudio.Shell.12.0" Version="[12.0]" />
    </Prerequisites>
 ...
</PackageManifest>
```

### <a name="option-use-the-designer-to-make-changes-to-the-vsix-extension-manifest"></a>选项：使用设计器对 VSIX 扩展清单进行更改

可以使用清单设计器中的新"先决条件"选项卡来选择先决条件，而不是直接编辑清单 XML，XML 将更新。

> [!Note]
> 清单设计器将仅允许你选择"组件"， (当前实例上安装的"工作负荷) 包"Visual Studio包" 。 如果需要为当前未安装的工作负荷、包或组件添加先决条件，请直接编辑清单 XML。

* 打开 *source.extension.vsixmanifest [Design]* 文件。
* 选择 **"先决条件"** 选项卡，然后按 **"新建"** 按钮。

   ![VSIX 清单设计器](media/vsix-manifest-designer.png)

* " **添加新的先决条件"** 窗口将打开。

   ![添加 vsix 先决条件](media/add-vsix-prerequisite.png)

* 单击"名称"下拉列表 **，** 然后选择所需的先决条件。
* 如有必要，请更新版本。

   > [!Note]
   > 版本字段将预先填充当前安装的组件的版本，其范围最多为 (，但不包括) 组件的下一个主要版本。

   ![添加 roslyn 先决条件](media/add-roslyn-prerequisite.png)

* 按“确定”。

## <a name="update-debug-settings-for-the-project"></a>更新项目的调试设置

如果要在 Visual Studio 试验实例中调试扩展，请确保"调试启动"操作的项目设置具有"启动外部程序： 值"设置为  >  Visual Studio 2017安装的devenv.exe文件。

它可能如下所示 *：C：\Program Files (x86) \Microsoft Visual Studio\2017\Enterprise\Common7\IDE\devenv.exe*

![启动外部程序](media/start-external-program.png)

> [!Note]
> 调试启动操作通常存储在 *.csproj.user* 文件中。 此文件通常包含在 *.gitignore* 文件中，因此，在提交到源代码管理时，通常不会与其他项目文件一起保存。 因此，如果从源代码管理中拉取解决方案，则项目很可能没有为"启动操作"设置任何值。 使用 Visual Studio 2017 创建的新 VSIX 项目将创建一个 *.csproj.user* 文件，其默认值指向当前 Visual Studio 安装目录。 但是，如果要迁移 VSIX v2 扩展，*则 .csproj.user* 文件可能包含对以前 Visual Studio 版本的安装目录的引用。 设置"调试 **开始**  >  **"操作的值** 将允许在尝试调试扩展Visual Studio启动正确的试验实例。

## <a name="check-that-the-extension-builds-correctly-as-a-vsix-v3"></a>检查扩展生成是否正确 (VSIX v3) 

* 生成 VSIX 项目。
* 解压缩生成的 VSIX。
  * 默认情况下，VSIX 文件位于 *bin/Debug* 或 *bin/Release* 中，作为 *[YourCustomExtension].vsix*。
  * 将 *.vsix* *重命名.zip* 以轻松查看内容。
* 检查是否存在三个文件：
  * *extension.vsixmanifest*
  * *manifest.js打开*
  * *catalog.js打开*

## <a name="check-when-all-required-prerequisites-are-installed"></a>检查何时安装了所有必需的必备组件

测试 VSIX 在安装了所有必需先决条件的计算机上安装成功。

> [!Note]
> 在安装任何扩展之前，请关闭所有 Visual Studio。

尝试安装扩展：

* 2017 Visual Studio 日

![2017 Visual Studio 上的 VSIX 安装程序](media/vsixinstaller-vs-2017.png)

* 可选：检查早期版本的 Visual Studio。
  * 证明向后兼容性。
  * 适用于 2012 Visual Studio 2012 年 Visual Studio 2013 Visual Studio 2015 年。
* 可选：检查 VSIX 安装程序版本检查器是否提供了一系列版本。
  * 包括以前版本的 Visual Studio (（如果已安装) ）。
  * 包括Visual Studio 2017 年。

如果Visual Studio最近打开，可能会看到如下所示的对话框：

![与正在运行的进程](media/vs-running-processes.png)

等待进程关闭或手动结束任务。 可以按列出的名称或括号中列出的 PID 查找进程。

> [!Note]
> 这些进程不会在实例实例运行时Visual Studio关闭。 确保已关闭计算机上所有 Visual Studio实例（包括来自其他用户的实例）然后继续重试。

## <a name="check-when-missing-the-required-prerequisites"></a>检查何时缺少所需的先决条件

* 尝试在具有 2017 Visual Studio的计算机上安装扩展，该计算机不包含上述先决条件 (定义的所有) 。
* 检查安装是否标识缺少的组件，并列出它们作为 VSIXInstaller 中的必备组件。
* 注意：如果需要随扩展一起安装任何先决条件，则需要提升权限。

![vsixinstaller 缺少先决条件](media/vsixinstaller-missing-prerequisite.png)

## <a name="decide-on-components"></a>确定组件

查找依赖项时，你会发现一个依赖项可以映射到多个组件。 若要确定应指定哪些依赖项作为先决条件，建议选择一个功能与扩展类似的组件，并考虑用户及其最有可能安装或不需要安装的组件类型。 我们还建议以以下方式生成扩展：所需先决条件仅满足允许扩展运行的最低要求;如果未检测到某些组件，对于其他功能，这些扩展将休眠。

为了提供进一步的指导，我们确定了一些常见的扩展类型及其建议的先决条件：

扩展类型 | 显示名称 | ID
--- | --- | ---
编辑器 | Visual Studio 核心编辑器 | Microsoft.VisualStudio.Component.CoreEditor
Roslyn | C# 和 Visual Basic | Microsoft.VisualStudio.Component.Roslyn.LanguageServices
WPF | 托管桌面工作负载核心 | Microsoft.VisualStudio.Component.ManagedDesktop.Core
调试器 | 实时调试器 | Microsoft.VisualStudio.Component.Debugger.JustInTime

## <a name="find-component-ids"></a>查找组件 Id

按 Visual Studio 产品排序的组件列表位于[2017 工作负荷和组件 id Visual Studio](../install/workload-and-component-ids.md?view=vs-2019&preserve-view=true)。 在清单中将这些组件 Id 用于必备 Id。

如果不确定哪个组件包含特定的二进制文件，请下载 [组件 > 二进制映射电子表格](https://aka.ms/vs2017componentid-binaries)。

### <a name="vs2017-componentbinarymappingxlsx"></a>vs2017-ComponentBinaryMapping.xlsx

Excel 工作表中有四列：**组件名称、组件名称**、**版本** 和 **二进制文件/文件名称**。   您可以使用筛选器搜索和查找特定组件和二进制文件。

对于所有引用，请首先确定哪些 VisualStudio 位于核心编辑器中 (CoreEditor) 组件。  至少需要将核心编辑器组件指定为所有扩展的必备组件。 对于不在核心编辑器中的引用，请在 " **二进制文件/文件名称** " 部分中添加筛选器，以查找具有这些引用的任意子集的组件。

示例：

* 如果你有一个调试器扩展，并且知道你的项目具有对 *VSDebugEng.dll* 和 *VSDebug.dll* 的引用，请在 " **二进制文件/文件名称** " 标头中单击 "筛选器" 按钮。  搜索 "VSDebugEng.dll"，然后选择 *"确定*"。  接下来，再次单击 " **二进制文件名称** " 标头中的 "筛选器" 按钮，然后搜索 "VSDebug.dll"。  选中 " **添加当前所选内容** " 复选框，然后选择 **"确定"**。  现在，浏览 **组件名称** ，查找与扩展类型最相关的组件。 在此示例中，你将选择实时调试器并将其添加到你的 source.extension.vsixmanifest。
* 如果你知道你的项目处理调试器元素，则可以在筛选器搜索框中搜索 "调试器"，以查看其名称中包含调试器的组件。

## <a name="specify-a-visual-studio-2017-release"></a>指定 Visual Studio 2017 版本

例如，如果你的扩展需要 Visual Studio 2017 的特定版本，则它依赖于15.3 中发布的一项功能，你必须在 VSIX **InstallationTarget** 中指定内部版本号。 例如，版本15.3 的生成号为 "15.0.26730.3"。 可在 [此处](../install/visual-studio-build-numbers-and-release-dates.md)查看生成编号的版本映射。 使用版本号 "15.3" 将不能正常工作。

如果扩展需要15.3 或更高版本，则需要将 **InstallationTarget 版本** 声明为 [15.0.26730.3，16.0) ：

```xml
<Installation>
  <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0.26730.3, 16.0)" />
</Installation>
```