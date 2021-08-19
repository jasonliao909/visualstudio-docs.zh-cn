---
title: 更新 Visual Studio 扩展
description: 了解如何更新 Visual Studio 扩展以使用 Visual Studio 2022。
ms.date: 06/08/2021
ms.topic: conceptual
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
monikerRange: vs-2022
ms.workload:
- vssdk
feedback_system: GitHub
ms.openlocfilehash: 08577adb3d79d01a514a73d2d9ef63b0c05d7f76
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094615"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>更新 Visual Studio 2022 的 Visual Studio 扩展

> [!IMPORTANT]
> 本指南中的建议旨在指导开发人员迁移扩展，这些扩展需要进行重大更改才能在 Visual Studio 2019 和2022中运行。 在这些情况下，建议使用两个 VSIX 项目和条件编译。
> 许多扩展都可以在 Visual Studio 2019 和2022中工作，并且不需要遵循本指南中有关现代化扩展的建议。
> 试用 Visual Studio 2022 中的扩展，并评估哪种选项最适合你的扩展。

可以按照本指南中所示更新扩展，使其与 Visual Studio 2022 Preview 一起使用。 Visual Studio 2022 Preview 是64位应用程序，并且在 VS SDK 中引入了一些重大更改。 本指南将指导你完成以下步骤：使用 Visual Studio 2022 的当前预览版来处理你的扩展，这样，在 Visual Studio 2022 达到 GA 之前，你的扩展可供用户安装。

## <a name="installing"></a>安装

从[Visual Studio 2022 预览版下载](https://visualstudio.microsoft.com/vs/preview/vs2022)Visual Studio 2022 预览版。

### <a name="extensions-written-in-a-net-language"></a>用 .NET 语言编写的扩展

托管扩展的 VS SDK 目标 Visual Studio 2022 NuGet： 

- VisualStudio) 元包中的[](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (版本 17. x 版本引入了所需的大多数或所有引用程序集。
- 应从 VSIX 项目引用[VSSDK.](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) x () 包的版本，以便它能够生成与2022兼容的 Visual Studio。

*必须* 用 "Any CPU" 或 "x64" 平台编译扩展。 "x86" 平台与 Visual Studio 2022 的64位进程不兼容。

### <a name="extensions-written-in-c"></a>用 c + + 编写的扩展

与使用 c + + 编译的扩展的 VS SDK 同样适用于已安装的 Visual Studio SDK。

*必须* 针对 Visual Studio 2022 SDK 和 amd64 专门编译扩展。

### <a name="update-your-extension-to-visual-studio-2022"></a>将扩展更新为 Visual Studio 2022

#### <a name="extensions-with-running-code"></a>运行代码的扩展

*必须* 专门针对 Visual Studio 2022 编译包含运行代码的扩展。 Visual Studio 2022 不会加载专门面向 Visual Studio 2022 的任何扩展。

了解如何将预 Visual Studio 2022 扩展迁移到 Visual Studio 2022：

1. [使项目实现现代化](#modernize-your-vsix-project)。
1. 将[您的源代码重构为共享项目](#use-shared-projects-for-multi-targeting)，以允许以 Visual Studio 2022 和更早版本为目标。
1. [添加 Visual Studio 2022 目标 VSIX 项目](#add-a-visual-studio-2022-target)，以及[包/程序集重新映射表](migrated-assemblies.md)。
1. [进行必要的代码调整](#handle-breaking-api-changes)。
1. [测试 Visual Studio 2022 扩展](#test-your-extension)。
1. [发布 Visual Studio 2022 扩展](#publish-your-extension)。

#### <a name="extensions-without-running-code"></a>不运行代码的扩展

不包含任何正在运行的代码 (例如，项目/项模板) *无* 需遵循上述步骤，包括两个不同 VSIXs 的生产。

相反，应修改一个 VSIX，使其 `source.extension.vsixmanifest` 文件声明两个安装目标，如下所示：

```xml
<Installation>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[15.0,17.0)">
      <ProductArchitecture>x86</ProductArchitecture>
   </InstallationTarget>
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
</Installation>
```

可以跳过本文中有关使用共享项目和多个 VSIXs 的步骤。 你可以继续 [测试](#test-your-extension)！

> [!NOTE]
> 如果要使用 Visual Studio 2022 预览版创作 *新* 的 Visual Studio 扩展，并希望 () 目标 Visual Studio 2019 或更早版本，请参阅 [此指南](target-previous-versions.md)。

### <a name="msbuild-tasks"></a>MSBuild 任务

如果你创作 MSBuild 任务，请注意，在 Visual Studio 2022 中，可能会将其加载到64位 MSBuild.exe 进程中。 如果任务需要32位进程才能运行，请参阅[本 MSBuild 文档](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters)，以确保 MSBuild 知道在32位进程中加载任务。

## <a name="modernize-your-vsix-project"></a>实现 VSIX 项目的现代化

将 Visual Studio 2022 支持添加到扩展之前，我们强烈建议在继续操作之前，先清理并现代化现有项目，其中包括：

1. [从 packages.config 迁移到 `PackageReference` ](/nuget/consume-packages/migrate-packages-config-to-package-reference)。

1. 将任何直接程序集 VS SDK 程序集引用替换为 PackageReference 项。

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > 只需将 *一个* PackageReference 替换为元包的 *多个* 程序集引用即可：
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" Version="..." />
   >```

   请确保选择与目标 Visual Studio 的最低版本匹配的包版本。

   某些对 VS SDK 不唯一的程序集 (例如，Newtonsoft.Json.dll) 在 Visual Studio 2022 之前可能已通过简单引用发现， `<Reference Include="Newtonsoft.Json" />` 但在 Visual Studio 2022 中，需要包引用，因为在 Visual Studio 2022 中，我们从 Visual Studio 的默认程序集搜索路径中删除了某些 MSBuild 的运行时和 SDK 目录。

   在从直接程序集引用切换到 NuGet 包引用时，可以选取其他程序集引用和分析器包，因为 NuGet 会自动安装依赖项的传递闭包。 这通常是正常的，但可能会导致在生成过程中标记其他警告。 完成这些警告并尽可能多地解决问题，并考虑禁止使用代码中区域无法解决的这些警告 `#pragma warning disable <id>` 。

## <a name="use-shared-projects-for-multi-targeting"></a>使用共享项目进行多目标

[共享项目](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)是 Visual Studio 2015 中引入的一种项目类型。 Visual Studio 中的共享项目允许在多个项目之间共享源代码文件，并使用条件编译符号和唯一的引用集以不同的方式进行构建。

由于 Visual Studio 2022 需要从所有以前的 VS 版本中使用一组不同的引用程序集，因此，我们的指导是使用共享项目方便多个目标扩展，以预 Visual Studio 2022 并 Visual Studio 2022 (和更高) 版本的和更高版本，从而提供代码共享但不同的引用。

在 Visual Studio 扩展的上下文中，可以为 Visual Studio 2022 和更高版本使用一个 vsix 项目，为 Visual Studio 2019 和更高版本创建一个 vsix 项目。 其中每个项目都只包含一个 `source.extension.vsixmanifest` ，包引用的是对 16. x sdk 或 17. x sdk 的引用。 这些 VSIX 项目还会对新的共享项目进行共享项目引用，该共享项目将托管可以在两个版本之间共享的所有源代码。

作为开始点，我们假设你已有一个面向 Visual Studio 2019 的 VSIX 项目，并且你希望你的扩展在 Visual Studio 2022 上工作。

所有这些步骤都可以通过 Visual Studio 2019 完成。

1. 如果尚未这样做，请在此更新过程中将 [项目现代化](#modernize-your-vsix-project) ，以简化步骤。

1. 为每个引用 VS SDK 的现有项目，将新的共享项目添加到解决方案。
   ![添加新的 Project 命令 ](media/update-visual-studio-extension/add-new-project.png)
    ![ 新建项目模板](media/update-visual-studio-extension/new-shared-project-template.png)

1. 将每个 VS SDK 引用项目中的引用添加到其共享项目对应项。
   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="添加共享项目引用" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 将所有源代码 (包括 .cs、.resx) ，从每个 VS SDK 引用项目到其共享项目对应项。
将 `source.extension.vsixmanifest` 文件保留在 VSIX 项目中。
   ![共享项目包含所有源文件](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. 应将) 和 .VSCT 文件 (的元数据文件移到共享目录，并将其作为链接文件添加到 VSIX 项目中。
   ![添加作为链接文件的元数据和 .VSCT 文件](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
    - 对于元数据文件，将 BuildAction 设置为， `Content` 并将 Include 包含在 VSIX 中 `true` 。

      ![在 VSIX 中包含元数据文件](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)
    - 对于 .VSCT 文件，将 BuildAction 设置为 `VSCTCompile` ，并且不包括在 VSIX 中。
      Visual Studio 可能会抱怨此设置不受支持，但你可以通过卸载项目并 `Content` 将更改为来手动更改生成操作`VSCTCompile`

    ```diff
    -<Content Include="..\SharedFiles\VSIXProject1Package.vsct">
    -  <Link>VSIXProject1Package.vsct</Link>
    -</Content>
    +<VSCTCompile Include="..\SharedFiles\VSIXProject1Package.vsct">
    +  <Link>VSIXProject1Package.vsct</Link>
    +  <ResourceName>Menus.ctmenu</ResourceName>
    +</VSCTCompile>
    ```

      ![将 .VSCT 文件设置为 VSCTCompile](media/update-visual-studio-extension/build-linked-vsct-files.png)

1.  (的) 生成项目，确认未引入任何新错误。

你的项目现已准备就绪，可以添加 Visual Studio 2022 支持。

## <a name="add-a-visual-studio-2022-target"></a>添加 Visual Studio 2022 目标

本文档假定你已完成将[Visual Studio 扩展与共享项目进行因式分解](#use-shared-projects-for-multi-targeting)的步骤。

继续使用以下步骤将 Visual Studio 2022 支持添加到扩展，这些步骤可能使用 Visual Studio 2019 完成：

1. 向解决方案添加新的 VSIX Project。 这将是面向 Visual Studio 2022 的项目。 删除模板附带的任何源代码，但 *保留该 `source.extension.vsixmanifest` 文件*。

1. 在新的 VSIX 项目上，将共享项目引用添加到 Visual Studio 2019 目标 VSIX 引用的同一共享项目。

   ![包含一个共享项目和两个 VSIX 项目的解决方案](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. 验证是否已正确生成新的 VSIX 项目。 你可能需要添加引用以匹配原始 VSIX 项目，以解决任何编译器错误。

1. 对于托管的 VS 扩展，使用 NuGet 程序包管理器或直接编辑项目文件，将 (或更早) 版本的包引用更新到 Visual Studio 2022 目标项目文件中的 17. x 包版本：

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   你将使用 nuget.org 中实际可用的版本。以前使用的是用于演示目的。

   在许多情况下，包 Id 已更改。 有关 Visual Studio 2022 中的更改列表，请参阅[包/程序集映射表](migrated-assemblies.md)。

   用 c + + 编写的扩展插件尚不具备可使用进行编译的 SDK。

1. 对于 c + + 项目，必须为 amd64 编译它们。 对于托管扩展，请考虑将你的项目从生成更改为面向任何 CPU `x64` ，以反映在 Visual Studio 2022 中，你的扩展始终在64位进程中加载。 `Any CPU` 很好，但如果引用任何仅 x64 本机二进制文件，则可能会产生警告。

   你的扩展可能在本机模块上具有的任何依赖项都必须从 x86 映像更新到 amd64 映像。

1. 编辑 `source.extension.vsixmanifest` 文件以反映目标为 Visual Studio 2022。 设置 `<InstallationTarget>` 标记以反映 2022 并指示 amd64 有效负载：

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   在 Visual Studio 2019 中，此文件的设计器不会公开新 `ProductArchitecture` 元素，因此，需要使用 xml 编辑器来完成此更改，该编辑器可通过 **解决方案资源管理器** 中的 "**打开方式**" 命令进行访问。

   此 `ProductArchitecture` 元素是关键元素。 Visual Studio 2022 *年 2* 月，如果没有扩展，将不会安装扩展。

   | 元素 | 值 | 说明 |
   | - | - | - |
   | ProductArchitecture | X86、AMD64 | 此 VSIX 支持的平台。 不区分大小写。 每个元素一个平台，每个 InstallTarget 一个元素。 对于低于 17.0 的产品版本，默认值为 x86，可以省略。  对于产品版本 17.0 及更大版本，此元素是必需的，并且没有默认值。 对于 Visual Studio 2022，此元素的唯一有效内容是"amd64"。 |

1. 在 source.extension.vsixmanifest 中做出任何其他必要的调整，以匹配面向 Visual Studio 2019 (（如果有) ）。 对于这两个扩展，清单的 元素中的 VSIX ID 必须 `Identity` 相同。这一点至关重要。

此时，你有一个面向 2022 Visual Studio VSIX 的扩展。 应生成面向 2022 Visual Studio VSIX 项目，并处理[出现的任何生成中断](#handle-breaking-api-changes)。 如果在面向 2022 Visual Studio VSIX 项目中没有生成中断，祝贺你：你已准备好进行测试！

## <a name="handle-breaking-api-changes"></a>处理中断性 API 更改

2022[年](breaking-api-list.md)Visual Studio API 发生了中断性变更，可能需要在早期版本中运行代码时更改代码。 请查看该文档，获取有关如何更新每个代码的代码的提示。

调整代码时，建议使用条件编译，以便代码[](#use-conditional-compilation-symbols)可以继续支持 2022 Visual Studio之前的代码，同时添加对 Visual Studio 2022 的支持。

获取面向 2022 Visual Studio的扩展生成时，请继续[测试](#test-your-extension)。

## <a name="use-conditional-compilation-symbols"></a>使用条件编译符号

如果要对 Visual Studio 2022 及更早版本使用相同的源代码，甚至使用相同的文件，可能需要使用条件编译，以便可以分叉代码以适应中断性变更。 条件编译是 C#、Visual Basic 和 C++ 语言的一项功能，可用于共享大多数代码，同时适应特定位置中的不同 API。

有关预处理器指令和条件编译符号用法的信息，请参阅 Microsoft docs #if [预处理器指令](/dotnet/csharp/language-reference/preprocessor-directives#conditional-compilation)。

面向 () Visual Studio版本的项目需要一个条件编译符号，该符号随后可用于为代码创建分支以使用不同的 API。 可以在项目属性页中设置条件编译符号，如下图所示：

![设置条件编译符号](media/update-visual-studio-extension/conditional-compilation-symbols.png)

请务必设置所有配置的编译符号，因为默认情况下，输入的符号可能仅适用于一个配置。

### <a name="c-techniques"></a>C \# 技术

然后，可以将该符号用作处理器前指令 () `#if` 如以下代码所示。 然后，可以分叉代码，处理不同版本之间的Visual Studio更改。

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
#if Visual Studio 2019
    shell.LoadUILibrary(myGuid, myFlags, out uint ptrLib);
#else
    shell.LoadUILibrary(myGuid, myFlags, out IntPtr ptrLib);
#endif
```

在某些情况下，只需使用 来避免对类型进行命名， `var` 从而避免区域 `#if` 需求。 上述代码片段也可以编写为：

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
    shell.LoadUILibrary(myGuid, myFlags, out var ptrLib);
```

使用 语法时，请注意如何使用下面所示文档中的语言服务上下文下拉列表来更改语法突出显示，以及语言服务提供的另一个帮助，将焦点放在扩展的一个目标 Visual Studio 版本与另一个扩展版本上。 `#if`

![共享项目中的条件编译](media/update-visual-studio-extension/conditional-compilation-if-region.png)

### <a name="xaml-sharing-techniques"></a>XAML 共享技术

XAML 没有预处理器，无法基于预处理器符号自定义内容。 复制和维护两个 XAML 页面，其中的内容在 Visual Studio 2022 和早期版本之间必须有所不同。

但是，在某些情况下，通过删除引用程序集的命名空间，在 Visual Studio 2022 和更早版本中存在于不同程序集中的类型的引用可能仍可以在一个 XAML 文件中表示：

```diff
-xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
-Value="{DynamicResource {x:Static vsui:TreeViewColors.SelectedItemActiveBrushKey}}"
+Value="{DynamicResource TreeViewColors.SelectedItemActiveBrushKey}"
```

## <a name="test-your-extension"></a>测试扩展

若要测试面向 2022 Visual Studio的扩展，需要安装 Visual Studio 2022 预览版。
在 2022 年预览版之前，无法对 Visual Studio 版本运行 64 Visual Studio扩展。

可以使用 Visual Studio 2022 预览版来生成和测试扩展，无论它们Visual Studio 2022 或更早版本。 从 2022 Visual Studio启动 VSIX 项目时，将启动 Visual Studio试验实例。

强烈建议使用希望扩展支持的每个Visual Studio版本进行测试。

现在，可以发布 [扩展了](#publish-your-extension)。

## <a name="publish-your-extension"></a>发布扩展

很好，因此你已向扩展Visual Studio 2022 目标并进行了测试。 现在，你已准备好将扩展发布给世界。

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

将扩展发布到[Visual Studio 市场](https://marketplace.visualstudio.com/)是让新用户查找和安装扩展的一种好方法。 无论扩展是Visual Studio 2022 年版本还是面向较旧的 VS 版本，市场都支持你。

将来，市场将允许你仅将多个 VSIX 上传到一个市场列表，从而上传面向 Visual Studio 2022 的 VSIX 和 2022 年Visual Studio VSIX。 使用 VS 扩展管理器时，用户将自动获得已安装的 VS 版本正确的 VSIX。

对于 2022 Visual Studio预览版，市场将仅支持每个市场列表的单个 VSIX 文件。 虽然Visual Studio 2022 年目前为预览版，但我们建议你为扩展单独Visual Studio 2022 年市场列表。 这样，你可根据需要Visual Studio 2022 扩展，而不会影响客户对早期版本的 Visual Studio。 还可以将扩展标记为"预览"，以设置这样一种预期：即使该不可靠性的来源是 2022 Visual Studio，它的可靠性也可能低于主流扩展。

### <a name="custom-installer"></a>自定义安装程序

如果生成 MSI/EXE 来安装扩展并生成 vsixinstaller.exe 以安装) 扩展的 (部分，请知道 Visual Studio 2022 中的 VSIX 安装程序已更新。 开发人员将需要使用 Visual Studio 2022 随附的 VSIX 安装程序版本来安装 2022 Visual Studio扩展。 Visual Studio 2022 中的 VSIX 安装程序还将安装适用于以前版本的 Visual Studio 的扩展，这些扩展与 Visual Studio 2022 并行安装在同一计算机上。

### <a name="network-share"></a>网络共享

可以通过 LAN 或其他任何方式共享扩展。 如果面向 Visual Studio 2022 和 Visual Studio 2022 之前版本，则需要单独共享多个 VSIX，并为用户提供文件名 (或将其放在唯一文件夹中) 以帮助用户根据已安装的 Visual Studio 版本了解要安装的 VSIX。

### <a name="other-considerations"></a>其他注意事项

#### <a name="dependencies"></a>依赖关系

如果 VSIX 通过 元素将另一个 VSIX 指定为依赖项，则每个引用的 VSIX 都需要安装在与 `<dependency>` VSIX 相同的目标和产品体系结构中。 如果从属 VSIX 不支持目标安装 Visual Studio，则 VSIX 将失败。 依赖的 VSIX 可以支持比你的目标更多的目标和体系结构，而不是更少。 此限制意味着具有依赖项的 VSIX 的部署和分发方法应反映其依赖项的部署和分发方法。

## <a name="q--a"></a>问题解答

**问**：我的扩展不需要任何互操作更改，因为它只提供数据 (例如模板) ，我能否创建包含 Visual Studio 2022 的扩展？

**答**：能！  有关详细信息 [，请参阅未运行代码](#extensions-without-running-code) 的扩展。

**问**：NuGet依赖关系引入旧的互操作程序集并导致类冲突。

**：** 将以下行添加到 .csproj 文件，以避免重复的程序集：

```xml
    <PackageReference Include="<Name of offending assembly>" ExcludeAssets="compile" PrivateAssets="all" />
```

这将阻止包引用从其他依赖项导入程序集的旧版本。

**问**：将源文件切换到共享项目Visual Studio，我的命令和热键无法正常使用。

**答**：图像优化器示例的步骤 [2.4](samples.md#step-2---refactor-source-code-into-a-shared-project) 演示如何将 VSCT 文件添加为链接项，以便将其编译到 VSCT 文件中。

## <a name="next-steps"></a>后续步骤

请遵循一个分步示例 [ImageOptimizer，](samples.md)其中提供了指向项目的链接，以及每个步骤的代码更改。
