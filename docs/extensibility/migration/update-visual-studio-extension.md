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
ms.openlocfilehash: 7969f08bef0a746df72de6a4582a06f7bdc1e685
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133514579"
---
# <a name="update-a-visual-studio-extension-for-visual-studio-2022"></a>更新 Visual Studio 2022 Visual Studio 扩展

> [!IMPORTANT]
> 本文中的建议可以指导开发人员迁移需要在 2019 和 2022 Visual Studio中正常工作的Visual Studio扩展。 在这种情况下，我们建议你有两个 VSIX 项目和条件编译。
>
> 许多扩展在 Visual Studio 2019 和 Visual Studio 2022 中都工作，但需要进行细微更改，无需遵循本文中有关扩展现代化的建议。 在 2022 Visual Studio中试用扩展，并评估最适合你的扩展的选项。

Visual Studio 2022 是一个 64 位应用程序，在 Visual Studio SDK 中引入了一些中断性变更。 本文指导你完成使扩展使用 2022 年 2 月的当前预览版Visual Studio步骤。 然后，可以在 2022 年 2 月Visual Studio安装扩展。

## <a name="install-visual-studio-and-compile-extensions"></a>安装Visual Studio并编译扩展

从 Visual Studio 2022 Visual Studio[安装 2022。](https://visualstudio.microsoft.com/downloads)

### <a name="extensions-written-in-a-net-language"></a>以 .NET 语言编写的扩展

面向托管Visual Studio 2022 Visual Studio 2022 的托管 SDK 专门NuGet：

- [Microsoft.VisualStudio.Sdk](https://www.nuget.org/packages/Microsoft.VisualStudio.Sdk/) (17.x) 元包引入你所需的大部分或所有引用程序集。
- 应从 VSIX 项目引用[Microsoft.VSSDK.BuildTools](https://www.nuget.org/packages/Microsoft.VSSDK.BuildTools/) (17.x) 包，以便它可以生成符合 Visual Studio 2022 的 VSIX。

即使未引用任何中断性变更，也必须使用"任何 **CPU"** 或 **"x64"** 平台编译扩展。  **x86** 平台与 2022 年 64 位Visual Studio不兼容。

### <a name="extensions-written-in-c"></a>用 C++ 编写的扩展

与Visual Studio一样，已安装的 Visual Studio SDK 中也提供了适用于使用 C++ 编译的扩展的 SDK。

即使不引用任何中断性变更，也必须针对 Visual Studio 2022 SDK 和 AMD64 专门编译扩展。 

### <a name="extensions-with-running-code"></a>具有运行代码的扩展

具有运行代码 *的扩展必须* 专门针对 Visual Studio 2022 进行编译。 Visual Studio 2022 将不会加载任何面向早期版本的 Visual Studio。

了解如何将早期版本的扩展迁移到 Visual Studio 2022 Visual Studio版本：

1. [使项目现代化](#modernize-your-vsix-project)。
1. [将源代码重构到共享](#use-shared-projects-for-multi-targeting)项目中，以面向 2022 Visual Studio版本。
1. [添加一Visual Studio 2022](#add-a-visual-studio-2022-target)目标 VSIX 项目和[一个包/程序集重新映射表](migrated-assemblies.md)。
1. [进行必要的代码调整](#handle-breaking-api-changes)。
1. [测试 Visual Studio 2022 扩展](#test-your-extension)。
1. [发布 2022 Visual Studio 2022 扩展](#publish-your-extension)。

### <a name="extensions-without-running-code"></a>无需运行代码的扩展

不包含任何正在运行的代码的扩展 (例如，项目或项模板) 执行上述步骤，包括两个不同的 VSIX 的生产。

相反，请修改一个 VSIX，以便其 `source.extension.vsixmanifest` 文件声明两个安装目标：

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

可以跳过本文中有关使用共享项目和多个 VSIX 的步骤。 可以继续 [测试](#test-your-extension)。

> [!NOTE]
> 如果要使用 Visual Studio 2022 创作新的 *Visual Studio* 扩展，并且还想要面向 Visual Studio 2019 或更早版本，请参阅 [本指南](target-previous-versions.md)。

### <a name="msbuild-tasks"></a>MSBuild 任务

如果创作MSBuild任务，请注意，在 Visual Studio 2022 中，它们很可能将加载到 64 位MSBuild.exe进程中。 如果任务需要 32 位进程才能运行，请参阅配置[](../../msbuild/how-to-configure-targets-and-tasks.md#usingtask-attributes-and-task-parameters)目标和任务以确保MSBuild 32 位进程中加载任务。

## <a name="modernize-your-vsix-project"></a>实现 VSIX 项目的现代化

在将 Visual Studio 2022 支持添加到扩展之前，我们强烈建议清理现有项目并使之现代化：

1. [从 packages.config 迁移到 `PackageReference` ](/nuget/consume-packages/migrate-packages-config-to-package-reference)。

1. 将任何直接Visual Studio SDK 程序集引用替换为 `PackageReference` 项：

   ```diff
   -<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   +<PackageReference Include="Microsoft.VisualStudio.OLE.Interop" Version="..." />
   ```

   > [!TIP]
   > 可以将许多 *程序集* 引用 *替换为元包* 的一 `PackageReference` 个实例：
   >
   >```diff
   >-<Reference Include="Microsoft.VisualStudio.OLE.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop" />
   >-<Reference Include="Microsoft.VisualStudio.Interop.8.0" />
   >+<PackageReference Include="Microsoft.VisualStudio.Sdk" Version="..." />
   >```

   请务必选择与目标版本的最低版本Visual Studio包版本。

例如，某些不是 Visual Studio SDK (唯一的程序集Newtonsoft.Json.dll)  `<Reference Include="Newtonsoft.Json" />` 2022 年 1 月之前通过简单Visual Studio发现。 但在 2022 Visual Studio，它们需要包引用。 原因是某些 Visual Studio 运行时和 SDK 目录已从 MSBuild 中的默认程序集搜索路径中删除。

在从直接程序集引用切换到NuGet包引用时，可能会选取其他程序集引用和分析器包，NuGet自动安装依赖项的可传递闭包。 这通常正常，但可能会导致生成期间出现其他警告。 处理这些警告并尽可能解决。 请考虑使用代码 `#pragma warning disable <id>` 内区域来禁止显示无法解决的警告。

## <a name="use-shared-projects-for-multi-targeting"></a>使用共享项目实现多目标

[共享项目](/xamarin/cross-platform/app-fundamentals/shared-projects?tabs=windows)是 2015 年 1 月Visual Studio项目类型。 使用 Visual Studio 中的共享项目，可以在多个项目之间共享源代码文件，并且使用条件编译符号和唯一引用集以不同方式生成。

Visual Studio 2022 年需要一组不同于所有早期版本的引用Visual Studio程序集。 因此，我们建议使用共享项目方便地将扩展多目标到 Visual Studio 2022、早期版本和更高版本。 此方法将提供代码共享，但提供不同的引用。

在 Visual Studio 扩展的上下文中，可以有一个适用于 Visual Studio 2022 和更高版本的 VSIX 项目，以及一个适用于 Visual Studio 2019 及更早版本的项目。 每个项目都只包含一个实例和对 `source.extension.vsixmanifest` 16.x SDK 或 17.x SDK 的包引用。 这些 VSIX 项目还将具有对新的共享项目的共享项目引用，该项目将托管可在两个版本之间共享的所有Visual Studio代码。

本部分假设已有一个面向 Visual Studio 2019 的 VSIX 项目，并且希望扩展在 2022 Visual Studio上工作。

可以使用 2019 年 1 月Visual Studio这些步骤：

1. 如果尚未这样做，请 [实现](#modernize-your-vsix-project) 项目的现代化，以便稍后在此更新过程中简化步骤。

1. 为引用 Visual Studio SDK 的每个现有项目将一个新的共享项目添加到解决方案。 右键单击解决方案，然后选择"**添加新**  >  **Project"。**

   ![显示用于添加新项目的选择的屏幕截图。](media/update-visual-studio-extension/add-new-project.png)

1. 在 **"添加新项目"对话框中**，搜索 **共享项目**，然后选择"**共享** 项目Project模板。

   ![屏幕截图显示搜索并选择"共享Project模板。](media/update-visual-studio-extension/new-shared-project-template.png)

1. 将每个引用 SDK Visual Studio项目的引用添加到其共享项目对应项。

   :::image type="content" source="media/update-visual-studio-extension/add-shared-project-reference.png" alt-text="显示用于添加共享项目引用的选择的屏幕截图。" lightbox="media/update-visual-studio-extension/add-shared-project-reference.png":::

1. 将包含 *.cs* (*.resx* 文件) 从每个 Visual Studio SDK 引用项目移动到其共享项目对应项。
在 VSIX *项目中保留 source.extension.vsixmanifest* 文件。

   ![显示包含所有源文件的共享项目的屏幕截图。](media/update-visual-studio-extension/source-files-in-shared-project.png)

1. 将元数据 (例如发行说明、许可证和图标) VSCT 文件移动到共享目录。 然后将它们作为链接文件添加到 VSIX 项目。 请注意，共享目录与共享项目分开。

   ![显示用于将元数据和 V S C T 文件添加为链接文件的选择的屏幕截图。](media/update-visual-studio-extension/add-linked-items-to-vsix.png)
   
   - 对于元数据文件，将"**生成操作"设置为****"内容"。** 将 **"在 VSIX 中包括"设置为** **True。**

     ![显示包含 VS I X 中的元数据文件的屏幕截图。](./media/update-visual-studio-extension/include-metadata-files-in-vsix.png)

   - 对于 VSCT 文件，将 **"生成操作"** 设置为 **"VSCTCompile"。** 将 **"在 VSIX 中包括"设置为** **False。** 
   
     ![显示 V S C T 文件的选定属性的屏幕截图。](media/update-visual-studio-extension/build-linked-vsct-files.png)
   
     如果Visual Studio此设置不受支持，可以通过卸载项目并更改为 来手动更改 `Content` 生成操作 `VSCTCompile` ：

     ```diff
     -<Content Include="..\SharedFiles\VSIXProject1Package.vsct">
     -  <Link>VSIXProject1Package.vsct</Link>
     -</Content>
     +<VSCTCompile Include="..\SharedFiles\VSIXProject1Package.vsct">
     +  <Link>VSIXProject1Package.vsct</Link>
     +  <ResourceName>Menus.ctmenu</ResourceName>
     +</VSCTCompile>
     ```

1. 生成项目以确认未引入任何错误。

现在，你的项目已准备好添加Visual Studio 2022 支持。

## <a name="add-a-visual-studio-2022-target"></a>添加 2022 Visual Studio 2022 目标

本部分假定你已完成将扩展与共享项目Visual Studio[因素的步骤](#use-shared-projects-for-multi-targeting)。

使用Visual Studio将 2022 支持添加到扩展。 可以使用 2019 Visual Studio它们。

1. 将新的 VSIX 项目添加到解决方案。 此项目面向 2022 Visual Studio。 删除模板提供的任何源代码，但保留 *source.extension.vsixmanifest* 文件。

1. 在新的 VSIX 项目上，添加对 2019 年目标 VSIX Visual Studio共享项目的引用。

   ![屏幕截图显示了一个解决方案，其中一个共享项目和两个 V S I X 项目。](media/update-visual-studio-extension/shared-project-with-two-heads.png)

1. 验证新的 VSIX 项目是否正确生成。 可能需要添加引用以匹配原始 VSIX 项目，以解决任何编译器错误。

1. 对于托管 Visual Studio 扩展，将包引用从 16.x (或更早版本) 更新到面向 Visual Studio 2022 的项目文件的 17.x 包版本。 使用 NuGet 程序包管理器或直接编辑项目文件：

    ```diff
    -<PackageReference Include="Microsoft.VisualStudio.SDK" Version="16.0.206" />
    +<PackageReference Include="Microsoft.VisualStudio.SDK" Version="17.0.0-preview.1" />
    -<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="16.10.32" />
    +<PackageReference Include="Microsoft.VSSDK.BuildTools" Version="17.0.63-preview.1" />
    ```

   上述代码中显示的版本仅供演示之用。 在代码中，使用[NuGet 网站](https://www.nuget.org/)中提供的版本。 

   在许多情况下，包 Id 已更改。 有关 Visual Studio 2022 中的更改列表，请参阅[包/程序集映射表](migrated-assemblies.md)。

   用 c + + 编写的扩展插件尚不具备可使用进行编译的 SDK。

1. 对于 c + + 项目，必须为 AMD64 编译扩展。 对于托管扩展，请考虑将你的项目更改为面向 **x64** 的 **任何 CPU** 。 这种更改可确保在 2022 Visual Studio，扩展始终在64位进程中加载。 **任何 CPU** 都很好，但如果引用任何仅 x64 本机二进制文件，则可能会产生警告。

   扩展可能在本机模块上具有的任何依赖项都必须从 x86 映像更新到 AMD64 映像。

1. 编辑 *source.extension.vsixmanifest* 文件，以反映 Visual Studio 2022 的目标。 将 `<InstallationTarget>` 标记设置为指示 Visual Studio 2022。 设置 `ProductArchitecture` 元素以指示 AMD64 负载。

   ```xml
   <InstallationTarget Id="Microsoft.VisualStudio.Community" Version="[17.0,18.0)">
      <ProductArchitecture>amd64</ProductArchitecture>
   </InstallationTarget>
   ```

   > [!IMPORTANT]
   > 在 Visual Studio 2019 中，此文件的设计器不公开新 `ProductArchitecture` 元素。 需要使用 XML 编辑器进行此更改。 若要访问 "XML 编辑器"，请访问解决方案资源管理器，然后选择 " **打开方式** " 命令。
   >
   > `ProductArchitecture`元素是关键元素。 Visual Studio 2022 不安装你的扩展。

   | 元素 | 值 | 说明 |
   | - | - | - |
   | `ProductArchitecture` | `x86`, `amd64` | 此 VSIX 支持的平台。 不区分大小写。 每个元素使用一个平台，每个实例使用一个元素 `InstallationTarget` 。 对于低于17.0 的产品版本，默认值为 `x86` ，可以省略。 对于产品版本17.0 及更高版本，此元素是必需的，并且没有默认值。 对于 Visual Studio 2022，此元素的唯一有效内容是 `amd64` 。 |

1. 如果任何) ，则在 *source.extension.vsixmanifest* 中进行任何其他必要的调整，以便与面向 Visual Studio 2019 (的任何其他调整。 

   如果要发布两个版本的扩展，每个版本都针对不同版本的 Visual Studio，请确保清单元素中的 VSIX ID `Identity` 对于每个扩展都是不同的。

此时，你有一个 Visual Studio 2022 目标扩展 VSIX。 应生成 Visual Studio 2022 目标 VSIX 项目，并[处理出现的任何生成中断](#handle-breaking-api-changes)。 如果在 Visual Studio 2022 目标 VSIX 项目中没有生成中断，恭喜！ 你已准备好进行测试。

## <a name="handle-breaking-api-changes"></a>处理重大 API 更改

中断 API 更改可能需要对 Visual Studio 早期版本上运行的代码进行更新。 有关如何更新代码的提示，请参阅[Visual Studio 2022 中的中断 API 更改](breaking-api-list.md)。

如果要调整代码，建议使用 [条件编译](#use-conditional-compilation-symbols)。 然后，你的代码可以继续支持早期版本的 Visual Studio，同时添加对 Visual Studio 2022 的支持。

当你获取 Visual Studio 2022 目标的扩展生成时，请继续进行[测试](#test-your-extension)。

## <a name="use-conditional-compilation-symbols"></a>使用条件编译符号

如果要为 Visual Studio 2022 及更早版本使用相同的源代码（甚至相同的文件），则可能需要使用条件编译。 然后，可以分叉代码以适应重大更改。 条件编译是 c #、Visual Basic 和 c + + 语言的一项功能。 它可用于共享大多数代码，同时适应特定位置的分歧 Api。

有关预处理器指令和条件编译符号的用法的详细信息，请参阅 [c # 预处理器指令](/dotnet/csharp/language-reference/preprocessor-directives#conditional-compilation)。

面向早期 Visual Studio 版本的项目将需要条件编译符号。 然后，可以使用此符号分叉代码以使用不同的 Api。 您可以在 "项目属性" 页上设置条件编译符号：

![显示用于输入条件编译符号的框的屏幕截图。](media/update-visual-studio-extension/conditional-compilation-symbols.png)

请确保为 **所有配置** 设置编译符号。 默认情况下，你输入的符号可能仅适用于一个配置。

### <a name="c-techniques"></a>C \# 方法

您可以使用编译符号作为预处理器指令 (`#if`) ，如下面的代码所示。 然后，可以分叉代码，处理 Visual Studio 版本之间的重大更改。

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

在某些情况下，可以使用 `var` 来避免对类型命名，并避免区域需要 `#if` 。 前面的代码段还可以编写为：

```cs
    Guid myGuid = new Guid("{633FBA02-719B-40E7-96BF-0899767CD104}");
    uint myFlags = 0;
    IVsShell shell = await AsyncServiceProvider.GlobalProvider.GetServiceAsync<SVsShell, IVsShell>();
    shell.LoadUILibrary(myGuid, myFlags, out var ptrLib);
```

使用 `#if` 语法时，请注意如何使用语言服务上下文的下拉列表来更改语法突出显示。 其他下拉列表可帮助语言服务将此扩展与另一个目标 Visual Studio 版本上的注意力集中在一起。

![在共享项目中显示条件编译的屏幕截图。](media/update-visual-studio-extension/conditional-compilation-if-region.png)

### <a name="xaml-sharing-techniques"></a>XAML 共享技术

XAML 没有预处理器来允许基于预处理器符号自定义内容。 你可能需要复制和维护两个 XAML 页面，它们的内容在 Visual Studio 2022 和更早版本之间不同。

在某些情况下，对于不同 Visual Studio 2022 和更早版本中的不同程序集中存在的类型的引用，可能仍可在一个 XAML 文件中表示。 删除引用该程序集的命名空间：

```diff
-xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
-Value="{DynamicResource {x:Static vsui:TreeViewColors.SelectedItemActiveBrushKey}}"
+Value="{DynamicResource TreeViewColors.SelectedItemActiveBrushKey}"
```

## <a name="test-your-extension"></a>测试扩展

若要测试针对 Visual Studio 2022 的扩展，需要安装 Visual Studio 2022。 你将无法在 Visual Studio 的早期版本上运行64位扩展。

你可以使用 Visual Studio 2022 来生成和测试你的扩展，无论它们是面向 Visual Studio 2022 还是早期版本。 当从 Visual Studio 2022 打开 VSIX 项目时，Visual Studio 的实验实例将打开。

我们强烈建议你测试需要该扩展插件支持的每个 Visual Studio 版本。

## <a name="publish-your-extension"></a>发布扩展

已将 Visual Studio 2022 目标添加到扩展并对其进行测试。 现在，你已准备好将世界各地的扩展发布到敬仰。

### <a name="visual-studio-marketplace"></a>Visual Studio Marketplace

将扩展发布到[Visual Studio Marketplace](https://marketplace.visualstudio.com/)是一种很好的方法，可让新用户查找和安装你的扩展。 无论你的扩展是以独占方式 Visual Studio 2022 还是以较旧 Visual Studio 版本为目标，都可以为你提供支持。

今后，Marketplace 允许将多个 VSIXs 上传到一个市场列表。 然后，你可以上传 Visual Studio 早期版本的 Visual Studio 2022 目标 vsix 和 vsix。 用户使用 Visual Studio 扩展管理器时，会自动获取已安装 Visual Studio 版本的适当 VSIX。

### <a name="custom-installer"></a>自定义安装程序

如果你构建一个 MSI 或 EXE 文件来安装扩展和生成 `vsixinstaller.exe` ，以便安装) 你的扩展 (的一部分，请注意 Visual Studio 2022 中的 VSIX 安装程序已更新。 开发人员需要使用 Visual Studio 2022 附带的 VSIX 安装程序版本来安装该版本 Visual Studio 的扩展。 

Visual Studio 2022 中的 VSIX 安装程序还会安装适用于在同一台计算机上具有 Visual Studio 2022 Visual Studio 的早期版本的适用扩展。

### <a name="network-share"></a>网络共享

你可以通过 LAN 或其他方式共享你的扩展。 如果以 Visual Studio 2022 及更早版本为目标，则需要单独共享多个 VSIXs。 为它们 (指定文件名，或将其放在唯一的文件夹中) 可帮助用户根据安装的 Visual Studio 版本了解要安装哪个 VSIX。

### <a name="dependencies"></a>依赖项

如果 VSIX 通过元素将其他 VSIXs 指定为依赖项 `<dependency>` ，则每个引用的 vsix 都需要安装在与 VSIX 相同的目标和产品体系结构中。 如果依赖 VSIX 不支持 Visual Studio 的目标安装，则 vsix 将失败。 

对于依赖 VSIX，支持比你的目标和体系结构更多的目标和体系结构是可以的。 此限制意味着，具有依赖关系的 VSIX 的部署和分发方法应反映其依赖项的依赖项。

## <a name="q--a"></a>问题解答

**问**：我的扩展不需要任何互操作性更改，因为它仅提供数据 (例如，模板) 。 是否可以创建一个也包括 Visual Studio 2022 的扩展插件？

**答**：能！ 有关此方面的信息，请参阅 [未运行代码的扩展](#extensions-without-running-code) 。

**问**： NuGet 依赖关系正在引入旧的互操作性程序集并导致冲突类。 应采取何种操作？

**：** 将以下行添加到 *.csproj* 文件以避免重复的程序集：

```xml
    <PackageReference Include="<Name of offending assembly>" ExcludeAssets="compile" PrivateAssets="all" />
```

此代码将阻止包引用从其他依赖项导入程序集的旧版本。

**问**：将源文件切换到共享项目Visual Studio，我的命令和热键停止在 Visual Studio 中工作。 应采取何种操作？

**答**：图像优化器示例的步骤 [2.4](samples.md#step-2---refactor-source-code-into-a-shared-project) 演示如何将 VSCT 文件添加为链接项，以便将其编译到 VSCT 文件中。

## <a name="next-steps"></a>后续步骤

请遵循一个分步示例 [ImageOptimizer，](samples.md)其中提供了指向项目的链接，以及每个步骤的代码更改。
