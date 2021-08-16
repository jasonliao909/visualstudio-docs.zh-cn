---
title: 如何往返扩展
description: 了解如何在 Visual Studio 2015 与 Visual Studio 2019 或 Visual Studio 2017 之间进行 Visual Studio 扩展性项目往返。
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
# <a name="how-to-make-extensions-compatible-with-visual-studio-20192017-and-visual-studio-2015"></a>如何：使扩展与 Visual Studio 2019/2017 和 Visual Studio 2015 兼容

本文档介绍了如何在 Visual Studio 2015 与 Visual Studio 2019 或 Visual Studio 2017 之间进行扩展。 完成此升级后，项目将能够在 Visual Studio 2015 和 Visual Studio 2019 或2017中打开、生成、安装和运行。 作为参考，可以在[VS SDK 扩展性示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)中找到可在 Visual Studio 2015 和 Visual Studio 2019 或2017之间往返的一些扩展。

如果只想在 Visual Studio 2019/2017 中生成，但希望输出 VSIX 在 Visual Studio 2015 和 Visual Studio 2019/2017 中运行，请参阅[扩展迁移文档](how-to-migrate-extensibility-projects-to-visual-studio-2017.md)。

> [!NOTE]
> 由于版本之间 Visual Studio 发生了更改，因此在一个版本中使用的某些功能在另一个版本中不起作用。 确保你尝试访问的功能在两个版本中均可用，或者扩展将产生意外的结果。

下面是你将在此文档中完成的步骤的大纲，用于往返 VSIX：

1. 导入正确的 NuGet 包。
2. 更新扩展清单：
    * 安装目标
    * 先决条件
3. 更新 .Csproj：
    * 更新 `<MinimumVisualStudioVersion>`。
    * 添加 `<VsixType>` 属性。
    * 添加调试属性 `($DevEnvDir)` 3 次。
    * 添加导入生成工具和目标的条件。

4. 生成和测试

## <a name="environment-setup"></a>环境设置

本文档假定计算机上已安装以下各项：

* 安装 VS SDK Visual Studio 2015
* 安装了扩展性工作负荷的 Visual Studio 2019 或2017

## <a name="recommended-approach"></a>推荐的方法

强烈建议使用 Visual Studio 2015 开始此次升级，而不是 Visual Studio 2019 或2017。 在 Visual Studio 2015 中进行开发的主要好处是确保不引用在 Visual Studio 2015 中不可用的程序集。 如果在 Visual Studio 2019 或2017中进行开发，则可能会导致依赖于仅存在于 Visual Studio 2019 或2017中的程序集的依赖关系。

## <a name="ensure-there-is-no-reference-to-projectjson"></a>确保没有对 project.js的引用

稍后在本文档中，我们将向你的 **.csproj* 文件中插入条件导入语句。 如果 NuGet 引用存储在 *的project.js* 中，则此操作不起作用。 因此，建议将所有 NuGet 引用移动到 *packages.config* 文件中。
如果项目包含文件 *上的project.js* ：

* 记下 *project.js上* 的引用。
* 从 **解决方案资源管理器** 中，从项目中删除文件 *project.js* 。 这会删除文件 *上的project.js* ，并将其从项目中删除。
* 将 NuGet 引用添加回项目：
  * 右键单击 **解决方案**，然后选择 "**管理解决方案 NuGet 包**"。
  * Visual Studio 会自动为你创建 *packages.config* 文件。

> [!NOTE]
> 如果你的项目包含 EnvDTE 包，则可能需要通过右键单击 " **引用** "，选择 " **添加引用** " 并添加相应的引用来添加它们。 在尝试生成项目时，使用 NuGet 包可能会产生错误。

## <a name="add-appropriate-build-tools"></a>添加适当的生成工具

我们需要确保添加使我们能够相应地生成和调试的生成工具。 Microsoft 为此名为 VisualStudio 的程序集创建了一个程序集。

若要在 Visual Studio 2015 和2019/2017 中生成和部署 VSIXv3，你将需要以下 NuGet 包：

版本 | 构建的工具
--- | ---
Visual Studio 2015 | VisualStudio. BuildTasks。
Visual Studio 2019 或2017 | VSSDK. BuildTool

为此，请执行以下操作：

* 将 NuGet 包添加到你的项目中。
* 如果你的项目不包含 VSSDK，请添加它。
* 确保 BuildTools 版本为 15. x 或更高版本。

## <a name="update-extension-manifest"></a>更新扩展清单

### <a name="1-installation-targets"></a>1. 安装目标

我们需要告诉 Visual Studio 要以何种版本来生成 VSIX。 通常，这些参考是 (14.0 Visual Studio 2015) ，版本 15.0 (Visual Studio 2017) 或版本 16.0 (Visual Studio 2019) 。 在我们的示例中，我们想要生成一个将为这两个版本都安装扩展的 VSIX，因此我们需要将这两个版本作为目标。 如果希望 VSIX 在14.0 以前的版本上生成并安装，可以通过设置较早的版本号来实现;但不再支持版本10.0 和更早版本。

* 在 Visual Studio 中打开 *source.extension.vsixmanifest* 文件。
* 打开 " **安装目标** " 选项卡。
* 将 **版本范围** 更改为 [14.0，17.0) 。 "[" 告诉 Visual Studio 包含14.0 以及它之后的所有版本。 ") " 通知 Visual Studio 包含版本17.0 之前的所有版本，但不包括版本。
* 保存所有更改并关闭 Visual Studio 的所有实例。

![安装目标映像](media/visual-studio-installation-targets-example.png)

### <a name="2-adding-prerequisites-to-the-extensionvsixmanifest-file"></a>2. 将先决条件添加到 *source.extension.vsixmanifest* 文件

需要 Visual Studio 核心编辑器作为必备组件。 打开 Visual Studio，并使用更新的清单设计器插入必备组件。

若要手动执行此操作：

* 在文件资源管理器中导航到项目目录。
* 使用文本编辑器打开 *source.extension.vsixmanifest* 文件。
* 添加以下标记：

```xml
<Prerequisites>
    <Prerequisite Id="Microsoft.VisualStudio.Component.CoreEditor" Version="[15.0,16.0)" DisplayName="Visual Studio core editor" />
</Prerequisites>
```

* 保存并关闭该文件。

> [!NOTE]
> 你可能需要手动编辑必备组件版本，以确保它与 Visual Studio 2019 或2017的所有版本兼容。 这是因为设计器将插入最小版本作为 Visual Studio 的当前版本 (例如，15.0.26208.0) 。 但是，因为其他用户可能有较早的版本，你需要手动将其编辑为15.0。

此时，清单文件应如下所示：

![先决条件示例](media/visual-studio-prerequisites-example.png)

## <a name="modify-the-project-file-myprojectcsproj"></a> (myproject 修改项目文件) 

在执行此步骤的同时，强烈建议对修改后的 .csproj 打开引用。 可在 [此处](https://github.com/Microsoft/VSSDK-Extensibility-Samples)找到几个示例。 选择任何扩展性示例，查找 *.csproj* 文件以供参考并执行以下步骤：

* 在 **文件资源管理器** 中导航到项目目录。
* 使用文本编辑器打开 *myproject* 文件。

### <a name="1-update-the-minimumvisualstudioversion"></a>1. 更新 I o n

* 将最小 visual studio 版本设置为 `$(VisualStudioVersion)` ，并为其添加一个条件语句。 如果这些标记不存在，请添加它们。 确保标记设置如下：

```xml
<VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">14.0</VisualStudioVersion>
<MinimumVisualStudioVersion>$(VisualStudioVersion)</MinimumVisualStudioVersion>
```

### <a name="2-add-the-vsixtype-property"></a>2. 添加 VsixType 属性。

* 将以下标记添加 `<VsixType>v3</VsixType>` 到属性组。

> [!NOTE]
> 建议在标记的下面添加 `<OutputType></OutputType>` 。

### <a name="3-add-the-debugging-properties"></a>3. 添加调试属性

* 添加以下属性组：

```xml
<PropertyGroup>
    <StartAction>Program</StartAction>
    <StartProgram>$(DevEnvDir)devenv.exe</StartProgram>
    <StartArguments>/rootsuffix Exp</StartArguments>
</PropertyGroup>
```

* 从 *.csproj* 文件和任何 *.csproj* 文件中删除以下代码示例的所有实例：

```xml
<StartAction>Program</StartAction>
<StartProgram>$(ProgramFiles)\Microsoft Visual Studio 14.0\Common7\IDE\devenv.exe</StartProgram>
<StartArguments>/rootsuffix Exp</StartArguments>
```

### <a name="4-add-conditions-to-the-build-tools-imports"></a>4. 向生成工具导入添加条件

* 将其他条件语句添加到 `<import>` 具有 VSSDK 引用的标记。 `'$(VisualStudioVersion)' != '14.0' And`在 condition 语句的前面插入。 这些语句将显示在 csproj 文件的页眉和页脚中。

例如：

```xml
<Import Project="packages\Microsoft.VSSDK.BuildTools.15.0.26201…" Condition="'$(VisualStudioVersion)' != '14.0' And Exists(…" />
```

* 将其他条件语句添加到具有 `<import>` Microsoft.VisualStudio.Sdk.BuildTasks.14.0 的标记。 在 `'$(VisualStudioVersion)' == '14.0' And` 条件语句的前面插入 。 这些语句将显示在 csproj 文件的页眉和页脚中。

例如：

```xml
<Import Project="packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" Condition="'$(VisualStudioVersion)' == '14.0' And Exists(…" />
```

* 向具有 `<Error>` Microsoft.VSSDK.BuildTools 引用的标记添加其他条件语句。 为此，请将 插入 condition `'$(VisualStudioVersion)' != '14.0' And` 语句的前面。 这些语句将显示在 csproj 文件的页脚中。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' != '14.0' And Exists('packages\Microsoft.VSSDK.BuildTools.15.0.26201…" />
```

* 将其他条件语句添加到具有 `<Error>` Microsoft.VisualStudio.Sdk.BuildTasks.14.0 的标记。 在 `'$(VisualStudioVersion)' == '14.0' And` 条件语句的前面插入 。 这些语句将显示在 csproj 文件的页脚中。

例如：

```xml
<Error Condition="'$(VisualStudioVersion)' == '14.0' And Exists('packages\Microsoft.VisualStudio.Sdk.BuildTasks.14.0.14.0…" />
```

* 保存 csproj 文件并将其关闭。 
  * 请注意，如果在解决方案中使用了多个项目，则通过使用项目上下文菜单上的"设置为启动 Project"将此项目设置为"启动 Project"，) 。 这可确保Visual Studio卸载后重新打开此项目。

## <a name="test-the-extension-installs-in-visual-studio-2015-and-visual-studio-2019-or-2017"></a>在 2015 和 2019 Visual Studio 2017 Visual Studio中测试扩展安装

此时，项目应已准备好生成可在 2015 和 Visual Studio 2017 Visual Studio安装的 VSIXv3。

* 在 2015 Visual Studio中打开项目。
* 生成项目，在输出中确认 VSIX 正确生成。
* 导航到项目目录。
* 打开 *\bin\Debug* 文件夹。
* 双击 VSIX 文件，在 2015 Visual Studio 2019/2017 Visual Studio安装扩展。
* 确保可以在"已安装的工具扩展和更新"部分  >  **看到** 扩展。 
* 尝试运行/使用扩展来检查其是否正常工作。

![查找 VSIX](media/finding-a-VSIX-example.png)

> [!NOTE]
> 如果项目停止响应并出现打开文件的消息，则强制关闭Visual Studio，导航到项目目录，显示隐藏文件夹，然后删除 *.vs* 文件夹。
