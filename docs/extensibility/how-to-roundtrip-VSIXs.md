---
title: 如何往返扩展
description: 了解如何在 2015 Visual Studio 2015 Visual Studio 2019 或 2017 Visual Studio之间往返扩展扩展Visual Studio项目。
ms.custom: SEO-VS-2020
ms.date: 06/25/2017
ms.topic: how-to
ms.assetid: 2d6cf53c-011e-4c9e-9935-417edca8c486
author: willbrown
ms.author: madsk
manager: justinclareburt
ms.workload:
- willbrown
ms.openlocfilehash: a5430271875917c890477a13e67056052ed382ee26546ef7536909866f0e8346
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401662"
---
# <a name="how-to-make-extensions-compatible-with-visual-studio-20192017-and-visual-studio-2015"></a>如何：使扩展与 2019/2017 Visual Studio 2015 Visual Studio兼容

本文档介绍如何使扩展性项目在 2015 年 Visual Studio 和 2019 Visual Studio 2017 Visual Studio之间往返。 完成此升级后，项目能够在 2015 和 2019 或 2017 Visual Studio 2015 Visual Studio中打开、生成、安装和运行。 作为参考，可在[VS SDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples)扩展性示例 找到一些可在 Visual Studio 2015 和 Visual Studio 2019 或 2017 之间往返的扩展。

如果只想在 Visual Studio 2019/2017 中生成，但希望输出 VSIX 在 Visual Studio 2015 和 Visual Studio 2019/2017 中运行，请参阅扩展迁移[文档](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

> [!NOTE]
> 由于版本Visual Studio更改，在一个版本中工作的一些操作在另一个版本中不起作用。 请确保你尝试访问的功能在这两个版本中都可用，否则扩展会获得意外的结果。

下面概述了本文档中往返 VSIX 的步骤：

1. 导入正确的NuGet包。
2. 更新扩展清单：
    * 安装目标
    * 先决条件
3. 更新 CSProj：
    * 更新 `<MinimumVisualStudioVersion>`。
    * 添加 `<VsixType>` 属性。
    * 添加调试属性 `($DevEnvDir)` 3 次。
    * 添加导入生成工具和目标的条件。

4. 生成和测试

## <a name="environment-setup"></a>环境设置

本文档假定计算机上已安装以下各项：

* Visual Studio VS SDK 的 2015 年 1 月
* Visual Studio扩展性工作负荷的 2019 或 2017 版本

## <a name="recommended-approach"></a>推荐的方法

强烈建议从 2015 Visual Studio开始此升级，而不是在 2019 Visual Studio 2017 年。 在 2015 Visual Studio开发的主要好处是确保不引用 2015 年 1 月Visual Studio程序集。 如果在 Visual Studio 2019 或 2017 中执行开发，则存在一种风险，即可能会引入对仅存在于 Visual Studio 2019 或 2017 中的程序集的依赖关系。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>确保没有对打开的project.js引用

本文档稍后将在 **.csproj* 文件中插入条件导入语句。 如果引用存储在 上的 NuGet中，project.js *不起作用*。 因此，建议将所有引用NuGet文件 *packages.config文件。*
如果项目包含一个 *project.js文件* ：

* 请记下 上project.js *中的引用*。
* 从 **解决方案资源管理器，** 从project.js *中删除文件* 上的文件。 这会删除 *project.js* 文件，并从项目中删除该文件。
* 将NuGet重新添加到项目中：
  * 右键单击"解决方案 **"，** 然后选择"**管理解决方案NuGet包"。**
  * Visual Studio自动 *创建packages.config文件*。

> [!NOTE]
> 如果项目包含 EnvDTE 包，可能需要右键单击"引用"，选择"添加引用"并添加相应的引用来添加它们。 在NuGet生成项目时，使用包可能会导致错误。

## <a name="add-appropriate-build-tools"></a>添加适当的生成工具

我们需要确保添加能够正确生成和调试的生成工具。 Microsoft 为此创建了名为 Microsoft.VisualStudio.Sdk.BuildTasks 的程序集。

若要在 Visual Studio 2015 和 2019/2017 中生成和部署 VSIXv3，需要以下NuGet包：

版本 | 生成工具
--- | ---
Visual Studio 2015 | Microsoft.VisualStudio.Sdk.BuildTasks.14.0
Visual Studio 2019 或 2017 年 | Microsoft.VSSDK.BuildTool

为此，请执行以下操作：

* 将NuGet Microsoft.VisualStudio.Sdk.BuildTasks.14.0 包添加到项目。
* 如果项目不包含 Microsoft.VSSDK.BuildTools，请添加它。
* 确保 Microsoft.VSSDK.BuildTools 版本为 15.x 或更高。

## <a name="update-extension-manifest"></a>更新扩展清单

### <a name="1-installation-targets"></a>1.安装目标

我们需要告知Visual Studio VSIX 的目标版本。 通常，这些引用可以是版本 14.0 (Visual Studio 2015) 、版本 15.0 (Visual Studio 2017) 或版本 16.0 (Visual Studio 2019) 。 在我们的案例中，我们想要生成一个 VSIX，用于安装这两个版本的扩展，因此我们需要同时面向这两个版本。 如果希望 VSIX 在低于 14.0 的版本上生成和安装，可以通过设置较早的版本号完成此操作;但是，不再支持版本 10.0 及更早版本。

* 打开 Visual Studio 中的 *source.extension.vsixmanifest* 文件。
* 打开" **安装目标"** 选项卡。
* 将版本 **范围更改为** [14.0， 17.0) 。 "["指示Visual Studio 14.0 及其后的所有版本。 ") "Visual Studio包括版本 17.0 之前（但不包括）的所有版本。
* 保存所有更改并关闭所有 Visual Studio。

![安装目标映像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2.将先决条件添加到 *extension.vsixmanifest* 文件

需要将Visual Studio编辑器作为先决条件。 打开Visual Studio，并使用更新的清单设计器插入先决条件。

若要手动执行此操作，

* 导航到项目中的项目文件资源管理器。
* 使用 *文本编辑器打开 extension.vsixmanifest* 文件。
* 添加以下标记：

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* 保存并关闭该文件。

> [!NOTE]
> 可能需要手动编辑先决条件版本，以确保它与 2019 或 2017 Visual Studio版本兼容。 这是因为设计器将插入最低版本作为当前版本的 Visual Studio (例如 15.0.26208.0) 。 但是，由于其他用户可能具有早期版本，因此需要手动编辑到 15.0。

此时，清单文件应如下所示：

![先决条件示例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a>修改项目文件 (myproject.csproj) 

强烈建议在执行此步骤时打开对已修改的 .csproj 的引用。 可在此处找到多个 [示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。 选择任意扩展性示例，找到 *.csproj* 文件供参考并执行以下步骤：

* 导航到 中的项目 **文件资源管理器。**
* 使用 *文本编辑器打开 myproject.csproj* 文件。

### <a name="1-update-the-minimumvisualstudioversion"></a>1.更新 MinimumVisualStudioVersion

* 将最低 visual Studio 版本设置为 `$(VisualStudioVersion)` ，并添加条件语句。 如果它们不存在，请添加这些标记。 确保标记设置如下：

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2.添加 VsixType 属性。

* 将以下标记 `<VsixType>v3</VsixType>` 添加到属性组。

> [!NOTE]
> 建议将此 添加到 标记 `<OutputType></OutputType>` 下方。

### <a name="3-add-the-debugging-properties"></a>3.添加调试属性

* 添加以下属性组：

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* 从 *.csproj* 文件和任何 *.csproj.user* 文件中删除以下代码示例的所有实例：

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4.向生成工具导入添加条件

* 向具有 `<import>` Microsoft.VSSDK.BuildTools 引用的标记添加其他条件语句。 在 `'$(VisualStudioVersion)' != '14.0' And` 条件语句的前面插入 。 这些语句将显示在 .csproj 文件的页眉和页脚中。

例如：

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* 将其他条件语句添加到 `<import>` 具有 VisualStudio 的标记中。 `'$(VisualStudioVersion)' == '14.0' And`在 condition 语句的前面插入。 这些语句将显示在 .csproj 文件的页眉和页脚中。

例如：

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* 将其他条件语句添加到 `<Error>` 具有 VSSDK 引用的标记。 为此，请 `'$(VisualStudioVersion)' != '14.0' And` 在 condition 语句的前面插入。 这些语句将显示在 .csproj 文件的页脚中。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* 将其他条件语句添加到 `<Error>` 具有 VisualStudio 的标记中。 `'$(VisualStudioVersion)' == '14.0' And`在 condition 语句的前面插入。 这些语句将显示在 .csproj 文件的页脚中。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* 保存 .csproj 文件并将其关闭。 
  * 请注意，如果您在解决方案中使用多个项目，则将此项目设置为 "启动 Project 通过使用项目上下文菜单上的" 设置为启动 Project ") 。 这可确保在卸载此项目后 Visual Studio 重新打开它。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2019-or-2017"></a>测试扩展安装 Visual Studio 2015 和 Visual Studio 2019 或2017

此时，项目应准备好生成可在 Visual Studio 2015 和 Visual Studio 2017 上安装的 VSIXv3。

* 在 Visual Studio 2015 中打开你的项目。
* 生成项目，并在输出中确认 VSIX 生成正确。
* 导航到项目目录。
* 打开 *\bin\Debug* 文件夹。
* 双击 VSIX 文件并在 Visual Studio 2015 和 Visual Studio 2019/2017 上安装扩展。
* 请确保在  >  "**已安装**" 部分的 "工具 **扩展和更新**" 中可以看到该扩展。
* 尝试运行/使用该扩展来检查它是否正常工作。

![查找 VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> 如果项目在 **打开文件** 时停止响应，则强制关闭 Visual Studio，导航到项目目录，显示隐藏文件夹，然后删除 *. vs* 文件夹。
