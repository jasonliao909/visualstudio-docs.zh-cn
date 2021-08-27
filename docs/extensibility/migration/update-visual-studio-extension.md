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
ms.openlocfilehash: bc76fa880814b0ae50ca6ad25d3f38849818b7d0
ms.sourcegitcommit: 42aec4a2ea6dec67dbe4c93bcf0fa1116a4b93d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2021
ms.locfileid: "122980636"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>更新 Visual Studio 2022 Visual Studio扩展

> [!IMPORTANT]
> 本指南中的建议旨在指导开发人员迁移需要在 2019 和 2022 Visual Studio进行重大更改的扩展。 在这种情况下，建议使用两个 VSIX 项目和条件编译。
> 许多扩展可以在 Visual Studio 2019 和 2022 中同时工作，但需要进行细微更改，无需遵循本指南中有关扩展现代化的建议。
> 在 2022 Visual Studio中试用扩展，并评估最适合你的扩展的选项。

可以按照本指南更新扩展Visual Studio 2022 预览版。 Visual Studio 2022 预览版是一个 64 位应用程序，在 VS SDK 中引入了一些中断性变更。 本指南指导你完成使扩展使用 Visual Studio 2022 的当前预览版所需的步骤，以便用户可以在 2022 年 2 月 2022 Visual Studio GA 之前准备好安装扩展。

## <a name="installing"></a>安装

从 Visual Studio 2022 预览版下载[安装 Visual Studio 2022 预览版](https://visualstudio.microsoft.com/vs/preview/vs2022)。

### <a name="extensions-written-in-a-net-language"></a>以 .NET 语言编写的扩展

面向托管扩展的 VISUAL STUDIO 2022 的 VS SDK 专门NuGet：

- [Microsoft.VisualStudio.Sdk](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (17.x) 元包引入你所需的大部分或所有引用程序集。
- 应从 VSIX 项目引用[Microsoft.VSSDK.BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) (17.x 版本) 包，以便它可以生成符合 Visual Studio 2022 的 VSIX。

即使不引用任何中断性变更，也必须使用"任何 CPU"或"x64"平台编译扩展。  "x86"平台与 Visual Studio 2022 的 64 位进程不兼容。

### <a name="extensions-written-in-c"></a>用 C++ 编写的扩展

与往常一样，已安装的 VISUAL STUDIO SDK 中也提供了使用 C++ 编译的 VS SDK for extensions。

即使不引用任何中断性变更，也必须针对 Visual Studio 2022 SDK 和 amd64 专门编译扩展。 

### <a name="update-your-extension-to-visual-studio-2022"></a>将扩展更新到 Visual Studio 2022

#### <a name="extensions-with-running-code"></a>具有运行代码的扩展

具有运行代码的 *扩展必须* 专门针对 Visual Studio 2022 进行编译。 Visual Studio 2022 将不会加载任何不以 2022 Visual Studio为目标的扩展。

了解如何将 2022 Visual Studio 2022 Visual Studio 2022：

1. [使项目现代化](#modernize-your-vsix-project)。
1. [将源代码重构到共享](#use-shared-projects-for-multi-targeting)项目中，以面向 2022 Visual Studio版本。
1. [添加一Visual Studio 2022](#add-a-visual-studio-2022-target)目标 VSIX 项目 ，以及[包/程序集重新映射表](migrated-assemblies.md)。
1. [进行必要的代码调整](#handle-breaking-api-changes)。
1. [测试 Visual Studio 2022 扩展](#test-your-extension)。
1. [发布 Visual Studio 2022 扩展](#publish-your-extension)。

#### <a name="extensions-without-running-code"></a>无需运行代码的扩展

不包含任何正在运行的代码的扩展 (例如，项目/项模板) 执行上述步骤（包括两个不同的 VSIX的生产）。

相反，应修改一个 VSIX，以便其 `source.extension.vsixmanifest` 文件声明两个安装目标，如下所示：

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

可以跳过本文中有关使用共享项目和多个 VSIX 的步骤。 可以继续 [测试](#test-your-extension)！

> [!NOTE]
> 如果要使用 Visual Studio 2022 预览版创作新的 *Visual Studio* 扩展，并且想要 () 目标 Visual Studio 2019 或更早版本，请查看 [本指南](target-previous-versions.md)。

### <a name="msbuild-tasks"></a>MSBuild 任务

如果创作MSBuild任务，请注意，在 Visual Studio 2022 中，它们更有可能加载到 64 位MSBuild.exe进程中。 如果任务需要 32 位进程才能运行，请参阅此MSBuild[](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters)文档，MSBuild知道在 32 位进程中加载任务。

## <a name="modernize-your-vsix-project"></a>实现 VSIX 项目的现代化

在将 Visual Studio 2022 支持添加到扩展之前，强烈建议先花时间清理现有项目并使之现代化，然后再进一步完成，包括：

1. [从 packages.config 迁移到 `PackageReference` ](/nuget/consume-packages/migrate-packages-config-to-package-reference)。

1. 将任何直接程序集 VS SDK 程序集引用替换为 PackageReference 项。

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > 只需将 *一* 个 PackageReference 替换为元包，就可以替换多个程序集引用： 
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" Version="..." />
   >```

   请务必选择与目标版本的最低版本Visual Studio包版本。

   某些不唯一于 VS SDK (例如 Newtonsoft.Json.dll) 的程序集可能在 Visual Studio 2022 之前通过简单引用发现，但在 Visual Studio 2022 中需要包引用，因为在 Visual Studio 2022 中，我们从 MSBuild 的默认程序集搜索路径中删除了一些 Visual Studio 运行时和 SDK 目录。 `<Reference Include="Newtonsoft.Json" />`

   在从直接程序集引用切换到NuGet包引用时，可能会选取其他程序集引用和分析器包，因为NuGet自动安装依赖项的可传递闭包。 这通常正常，但可能会导致在生成过程中标记其他警告。 请解决这些警告并尽可能多地解决，并考虑取消使用代码内区域无法解决的 `#pragma warning disable <id>` 这些警告。

## <a name="use-shared-projects-for-multi-targeting"></a>使用共享项目实现多目标

[共享项目](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)是 2015 年 1 月Visual Studio项目类型。 使用 Visual Studio 中的共享项目，可以在多个项目之间共享源代码文件，并使用不同的条件编译符号和唯一引用集生成源代码文件。

由于 Visual Studio 2022 需要一组不同于所有先前 VS 版本的引用程序集，因此，我们的指南是使用共享项目方便地将扩展多目标到 Visual Studio 2022 和 Visual Studio 2022 (及更高版本) ，从而提供代码共享，但提供不同的引用。

在 Visual Studio 扩展的上下文中，可以有一个适用于 Visual Studio 2022 和更高版本的 VSIX 项目，以及一个适用于 Visual Studio 2019 及更早版本的项目。 每个项目都只包含 一个 ，并且包 `source.extension.vsixmanifest` 引用 16.x SDK 或 17.x SDK。 这些 VSIX 项目还将具有对新的共享项目的共享项目引用，该项目将托管可在两个 VS 版本之间共享的所有源代码。

首先，对于本文档，我们假设你已有一个面向 Visual Studio 2019 的 VSIX 项目，并且希望你的扩展在 2022 Visual Studio工作。

所有这些步骤都可以在 2019 Visual Studio完成。

1. 如果尚未这样做，请 [现代化项目](#modernize-your-vsix-project) ，以便稍后在此更新过程中简化步骤。

1. 为引用 VS SDK 的每个现有项目向解决方案添加新的共享项目。
   !["添加新 ](media/update-visual-studio-extension/add-new-project.png)
    ![ Project"命令"新建项目模板"](media/update-visual-studio-extension/new-shared-project-template.png)

1. 将引用从每个 VS SDK 引用项目添加到其共享项目对应项。
   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="添加共享项目引用" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 将包含 .cs、.resx (的所有源代码从) VS SDK 引用项目移动到其共享项目对应项。
将 `source.extension.vsixmanifest` 文件保留于 VSIX 项目中。
   ![共享项目包含所有源文件](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. 元数据 (发行说明、许可证、图标等) 和 VSCT 文件应移动到共享目录，并作为链接文件添加到 VSIX 项目。
   ![将元数据和 VSCT 文件添加为链接文件](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
    - 对于元数据文件，将 BuildAction 设置为 `Content` ，将"在 VSIX 中包括"设置为 `true` 。

      ![在 VSIX 中包括元数据文件](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)
    - 对于 VSCT 文件，将 BuildAction 设置为 且 `VSCTCompile` 不包含在 VSIX 中。
      Visual Studio可能会指出此设置不受支持，但可以通过卸载项目并更改为 来手动更改生成 `Content` 操作`VSCTCompile`

    ```diff
    -<Content Include="..\SharedFiles\VSIXProject1Package.vsct">
    -  <Link>VSIXProject1Package.vsct</Link>
    -</Content>
    +<VSCTCompile Include="..\SharedFiles\VSIXProject1Package.vsct">
    +  <Link>VSIXProject1Package.vsct</Link>
    +  <ResourceName>Menus.ctmenu</ResourceName>
    +</VSCTCompile>
    ```

      ![将 VSCT 文件设置为 VSCTCompile](media/update-visual-studio-extension/build-linked-vsct-files.png)

1. 生成项目 () 以确认未引入任何新错误。

现在，你的项目已准备好添加Visual Studio 2022 支持。

## <a name="add-a-visual-studio-2022-target"></a>添加一Visual Studio 2022 目标

本文档假定你已完成将扩展Visual Studio[共享项目的步骤](#use-shared-projects-for-multi-targeting)。

继续执行以下步骤Visual Studio 2022 支持添加到扩展，这些步骤可能使用 2019 Visual Studio完成：

1. 将新的 VSIX Project添加到解决方案。 这将是面向 2022 Visual Studio的项目。 删除模板提供的任何源代码，但 *保留 `source.extension.vsixmanifest` 文件*。

1. 在新的 VSIX 项目上，将共享项目引用添加到 2019 Visual Studio VSIX 引用的共享项目。

   ![具有一个共享项目和两个 VSIX 项目的解决方案](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. 验证新的 VSIX 项目是否正确生成。 可能需要添加引用以匹配原始 VSIX 项目，以解决任何编译器错误。

1. 对于托管 VS 扩展，使用 NuGet 程序包管理器 将包引用从 16.x (或更早版本) 更新到 Visual Studio 2022 目标项目文件的 17.x 包版本，或直接编辑项目文件：

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   你将使用实际可从 nuget.org。以前使用过，仅用于演示目的。

   在许多情况下，包的 ID 已更改。 有关 2022 年 2 月中的更改列表，请参阅包/程序集Visual Studio表。 [](migrated-assemblies.md)

   用 C++ 编写的扩展尚没有可用于编译的 SDK。

1. 对于 C++ 项目，必须针对 amd64 编译它们。 对于托管扩展，请考虑将项目从"针对任何 CPU 生成"更改为目标，以反映在 Visual Studio 2022 年，扩展始终在 `x64` 64 位进程中加载。 `Any CPU` 也可以，但如果引用任何仅 x64 的本机二进制文件，则可能会产生警告。

   扩展对本机模块的任何依赖项必须从 x86 映像更新为 amd64 映像。

1. 编辑 `source.extension.vsixmanifest` 文件以反映目标为 Visual Studio 2022。 设置 `<InstallationTarget>` 标记以反映 2022 并指示 amd64 有效负载：

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   在 Visual Studio 2019 中，此文件的设计器不会公开新元素，因此此更改将需要使用 xml 编辑器完成，可以通过 解决方案资源管理器 中的 `ProductArchitecture` **Open With** **命令访问** 该编辑器。

   此 `ProductArchitecture` 元素至关重要。 Visual Studio 2022 年 *2* 月不会在没有扩展的情况下安装扩展。

   | 元素 | 值 | 描述 |
   | - | - | - |
   | ProductArchitecture | X86、AMD64 | 此 VSIX 支持的平台。 不区分大小写。 每个元素一个平台，每个 InstallTarget 一个元素。 对于低于 17.0 的产品版本，默认值为 x86，可以省略。  对于产品版本 17.0 及更大版本，此元素是必需的，并且没有默认值。 对于 Visual Studio 2022，此元素的唯一有效内容是"amd64"。 |

1. 在 source.extension.vsixmanifest 中做出任何其他必要的调整，以匹配面向 Visual Studio 2019 (（如果有) ）。 如果要发布 2 个不同版本的扩展，每个版本都面向不同版本的 VS，则两个扩展的清单元素中的 VSIX ID 必须不同。 `Identity`

此时，你有一个面向 2022 Visual Studio VSIX 的扩展。 应生成面向 2022 Visual Studio VSIX 项目，并处理显示 的任何[生成中断](#handle-breaking-api-changes)。 如果在面向 2022 Visual Studio VSIX 项目中没有生成中断，祝贺你：你已准备好进行测试！

## <a name="handle-breaking-api-changes"></a>处理中断性 API 更改

2022[年](breaking-api-list.md)Visual Studio API 发生了中断性变更，可能需要在早期版本中运行代码时更改代码。 请查看该文档，获取有关如何更新每个代码的代码的提示。

调整代码时，建议使用条件编译，以便代码[](#use-conditional-compilation-symbols)可以继续支持 2022 Visual Studio之前的代码，同时添加对 Visual Studio 2022 的支持。

获取面向 2022 Visual Studio的扩展生成时，请继续[测试](#test-your-extension)。

## <a name="use-conditional-compilation-symbols"></a>使用条件编译符号

如果要对 Visual Studio 2022 及更早版本使用相同的源代码，甚至使用相同的文件，可能需要使用条件编译，以便可以分叉代码以适应中断性变更。 条件编译是 C#、Visual Basic 和 C++ 语言的一项功能，可用于共享大多数代码，同时适应特定位置中的不同 API。

有关预处理器指令和条件编译符号用法的信息，请参阅 Microsoft docs [#if预处理器指令](/dotnet/csharp/language-reference/preprocessor-directives#conditional-compilation)。

面向 () Visual Studio 版本的项目需要一个条件编译符号，该符号随后可用于为代码创建分支以使用不同的 API。 可以在项目属性页中设置条件编译符号，如下图所示：

![设置条件编译符号](media/update-visual-studio-extension/conditional-compilation-symbols.png)

请务必设置所有配置的编译符号，因为默认情况下，输入的符号可能仅适用于一个配置。

### <a name="c-techniques"></a>C \# 技术

然后，可以将该符号用作预处理器指令 () `#if` 如以下代码所示。 然后，可以分叉代码来处理不同版本之间的中断性Visual Studio变化。

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
#if Dev16
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

使用 语法时，请注意如何使用下面所示文档中的语言服务上下文下拉列表更改语法突出显示，以及语言服务提供的另一个帮助，将焦点放在扩展的一个目标 Visual Studio 版本与另一个扩展版本上。 `#if`

![共享项目中的条件编译](media/update-visual-studio-extension/conditional-compilation-if-region.png)

### <a name="xaml-sharing-techniques"></a>XAML 共享技术

XAML 没有预处理器，无法基于预处理器符号自定义内容。 复制和维护两个 XAML 页面，其中其内容在 Visual Studio 2022 和早期版本之间必须有所不同。

但是，在某些情况下，通过删除引用程序集的命名空间，在 Visual Studio 2022 和更早版本中存在于不同程序集中的类型的引用仍可在一个 XAML 文件中表示：

```diff
-xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
-Value="{DynamicResource {x:Static vsui:TreeViewColors.SelectedItemActiveBrushKey}}"
+Value="{DynamicResource TreeViewColors.SelectedItemActiveBrushKey}"
```

## <a name="test-your-extension"></a>测试扩展

若要测试面向 Visual Studio 2022 的扩展，需要安装 Visual Studio 2022 预览版。
在 2022 年预览版之前，无法对 Visual Studio 版本运行 64 Visual Studio扩展。

可以使用 Visual Studio 2022 预览版来生成和测试扩展，无论它们Visual Studio 2022 或更早版本。 从 2022 Visual Studio启动 VSIX 项目时，将启动 Visual Studio试验实例。

强烈建议使用希望扩展支持的每个Visual Studio版本进行测试。

现在，可以发布 [扩展了](#publish-your-extension)。

## <a name="publish-your-extension"></a>发布扩展

很好，因此你已向扩展Visual Studio 2022 目标并进行了测试。 现在，你已准备好将扩展发布给世界。

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

将扩展发布到[Visual Studio 市场](https://marketplace.visualstudio.com/)是让新用户查找和安装扩展的一种好方法。 无论扩展是Visual Studio 2022 年版本还是面向较旧的 VS 版本，市场都支持你。

将来，市场将允许你将多个 VSIX 仅上传到一个市场列表，从而允许上传面向 Visual Studio 2022 的 VSIX 和 2022 年Visual Studio VSIX。 使用 VS 扩展管理器时，用户将自动获得已安装的 VS 版本正确的 VSIX。

对于 2022 Visual Studio预览版，市场将仅支持每个市场列表的单个 VSIX 文件。 尽管 Visual Studio 2022 年是预览版，但我们建议你为扩展单独Visual Studio 2022 年市场列表。 这样，你可根据需要Visual Studio 2022 扩展，而不会影响客户对早期版本的 Visual Studio。 还可以将扩展标记为"预览"，以设置这样一种预期：即使该不可靠性的来源是 2022 Visual Studio，它的可靠性也可能低于主流扩展。

### <a name="custom-installer"></a>自定义安装程序

如果生成 MSI/EXE 来安装扩展并生成 vsixinstaller.exe 以安装 () 扩展的) 部分，请知道 Visual Studio 2022 中的 VSIX 安装程序已更新。 开发人员将需要使用 Visual Studio 2022 随附的 VSIX 安装程序版本来安装 2022 Visual Studio扩展。 Visual Studio 2022 中的 VSIX 安装程序还将安装适用于以前版本的 Visual Studio 的扩展，这些扩展与 Visual Studio 2022 并行安装在同一计算机上。

### <a name="network-share"></a>网络共享

可以通过 LAN 或其他任何方式共享扩展。 如果面向 Visual Studio 2022 和 Visual Studio 2022 之前版本，则需要单独共享多个 VSIX，并指定文件名 (或将其放在唯一文件夹中) 以帮助用户根据已安装的 Visual Studio 版本了解要安装的 VSIX。

### <a name="other-considerations"></a>其他注意事项

#### <a name="dependencies"></a>依赖项

如果 VSIX 通过 元素将另一个 VSIX 指定为依赖项，则每个引用的 VSIX 都需要安装在与 `<dependency>` VSIX 相同的目标和产品体系结构中。 如果依赖的 VSIX 不支持目标安装 Visual Studio，则 VSIX 将失败。 依赖的 VSIX 可以支持比你的目标更多的目标和体系结构，而不是更少。 此限制意味着具有依赖项的 VSIX 的部署和分发方法应反映其依赖项的部署和分发方法。

## <a name="q--a"></a>问题解答

**问**：我的扩展不需要任何互操作更改，因为它只提供数据 (例如模板) ，我能否创建包含 Visual Studio 2022 的单个扩展？

**答**：能！  有关详细信息 [，请参阅未运行代码](#extensions-without-running-code) 的扩展。

**问**：NuGet引入旧的互操作程序集并导致类冲突。

**：** 将以下行添加到 .csproj 文件以避免重复的程序集：

```xml
    <PackageReference Include="<Name of offending assembly>" ExcludeAssets="compile" PrivateAssets="all" />
```

这将阻止包引用从其他依赖项导入程序集的旧版本。

**问**：将源文件切换到共享项目后，Visual Studio和热键无法正常使用。

**答**：图像优化器示例的步骤 [2.4](samples.md#step-2---refactor-source-code-into-a-shared-project) 演示如何将 VSCT 文件添加为链接项，以便将其编译到 VSCT 文件中。

## <a name="next-steps"></a>后续步骤

请遵循一个分步示例 [ImageOptimizer，](samples.md)其中提供了指向项目的链接，以及每个步骤的代码更改。
