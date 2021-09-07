---
title: 创建软件开发工具包|Microsoft Docs
description: 了解 SDK 的常规基础结构，以及如何创建平台 SDK 和扩展 SDK。
ms.custom: SEO-VS-2020
ms.date: 08/31/2021
ms.topic: how-to
ms.assetid: 8496afb4-1573-4585-ac67-c3d58b568a12
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 88a888bfcaa868fba0b259fbb7037d30f756784e
ms.sourcegitcommit: 8d529614652d902f265de4a6d9419bc0dfab97ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2021
ms.locfileid: "123501595"
---
# <a name="create-a-software-development-kit"></a>创建软件开发工具包

SDK (sdk) 是一组 API，可以在其中作为单个项引用Visual Studio。 " **引用** 管理器"对话框列出与项目相关的所有 SDK。 将 SDK 添加到项目时，API 可在 Visual Studio。

有两种类型的 SDK：

- 平台 SDK 是开发平台应用必需的组件。 例如， [!INCLUDE[win81](../debugger/includes/win81_md.md)] 开发应用需要 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] SDK。

- 扩展 SDK 是扩展平台的可选组件，但不是必需的组件，用于开发该平台的应用。

以下部分介绍 SDK 的常规基础结构，以及如何创建平台 SDK 和扩展 SDK。

## <a name="platform-sdks"></a>平台 SDK

开发平台应用需要平台 SDK。 例如 [!INCLUDE[win81](../debugger/includes/win81_md.md)] ，SDK 是开发 的应用所需的 [!INCLUDE[win81](../debugger/includes/win81_md.md)] 。

### <a name="installation"></a>安装

所有平台 SDK 都将安装在 *HKLM\Software\Microsoft\Microsoft SDK \\ [TPI]\v[TPV] \\ @InstallationFolder = [SDK 根]* 上。 相应地 [!INCLUDE[win81](../debugger/includes/win81_md.md)] ，SDK 安装在 *HKLM\Software\Microsoft\Microsoft SDKs\Windows\v8.1 中*。

### <a name="layout"></a>Layout

平台 SDK 具有以下布局：

```
\[InstallationFolder root]
            SDKManifest.xml
            \References
                  \[config]
                        \[arch]
            \DesignTime
                  \[config]
                        \[arch]
```

| 节点 | 描述 |
|------------------------| - |
| *References* 文件夹 | 包含包含可编码的 API 的二进制文件。 这些元数据可能包括Windows或 (WinMD) 元数据。 |
| *DesignTime* 文件夹 | 包含仅在预运行/调试时需要的文件。 这些可能包括 XML 文档、库、标头、工具箱设计时二进制文件MSBuild项目等<br /><br /> 理想情况下，XML 文档将放置在 *\DesignTime* 文件夹中，但用于引用的 XML 文档将继续与引用文件一起放置在 Visual Studio。 例如，引用 <em>\References \\ [config] \\ [arch]\sample.dll</em> 的 XML 文档将为 *\References \\ [config] \\ [arch]\sample.xml，* 而该文档的本地化版本将为 *\References \\ [config] \\ [arch] \\ [locale]\sample.xml*。 |
| *配置* 文件夹 | 只能有三个文件夹："*调试"、"**零* 售"和 *"CommonConfiguration"。* SDK 作者可以将文件放在 *CommonConfiguration* 下（如果应该使用同一组 SDK 文件，而不考虑 SDK 使用者将面向的配置）。 |
| *体系结构* 文件夹 | 任何支持的 *体系结构* 文件夹都可以存在。 Visual Studio支持以下体系结构：x86、x64、ARM 和 neutral。 注意：Win32 映射到 x86，AnyCPU 映射到中性。<br /><br /> MSBuild平台 SDK 的 *\CommonConfiguration\neutral* 下查找。 |
| *SDKManifest.xml* | 此文件介绍如何Visual Studio SDK。 查看 的 SDK 清单 [!INCLUDE[win81](../debugger/includes/win81_md.md)] ：<br /><br /> `<FileList             DisplayName = "Windows"             PlatformIdentity = "Windows, version=8.1"             TargetFramework = ".NET for Windows Store apps, version=v4.5.1; .NET Framework, version=v4.5.1"             MinVSVersion = "14.0">              <File Reference = "Windows.winmd">                <ToolboxItems VSCategory = "Toolbox.Default" />             </File> </FileList>`<br /><br /> **DisplayName：** 对象浏览器在"浏览"列表中显示的值。<br /><br /> **PlatformIdentity：** 存在此属性会Visual Studio SDK MSBuild SDK 是平台 SDK，并且不应在本地复制从它添加的引用。<br /><br /> **TargetFramework：** 此属性由 Visual Studio，以确保只有面向此属性的值中指定的相同框架的项目才能使用 SDK。<br /><br /> **MinVSVersion：** 此属性由 Visual Studio用于仅使用应用于它的 SDK。<br /><br /> **参考：** 必须仅为包含控件的引用指定此属性。 若要了解如何指定引用是否包含控件，请参阅下文。 |

## <a name="extension-sdks"></a>扩展 SDK

以下部分介绍部署扩展 SDK 需要执行哪些操作。

### <a name="installation"></a>安装

无需指定注册表项即可为特定用户或所有用户安装扩展 SDK。 若要为所有用户安装 SDK，请使用以下路径：

*%Program Files%\Microsoft SDK \<target platform\> \v<平台版本号 \> \ExtensionSDKs*

对于特定于用户的安装，请使用以下路径：

*%USERPROFILE%\AppData\Local\Microsoft SDK \<target platform\> \v<平台版本号 \> \ExtensionSDKs*

如果要使用不同的位置，必须执行两项操作之一：

1. 在注册表项中指定它：

     **HKLM\Software\Microsoft\Microsoft SDKs \<target platform> \v<平台版本号 \> \ExtensionSDKs\<SDKName>\<SDKVersion>**\

     并添加一 (默认值) 值为 的子项 `<path to SDK><SDKName><SDKVersion>` 。

2. 将 MSBuild `SDKReferenceDirectoryRoot` 属性添加到项目文件。 此属性的值是要引用的扩展 SDK 所在的目录的分号分隔列表。

### <a name="installation-layout"></a>安装布局

扩展 SDK 具有以下安装布局：

```
\<ExtensionSDKs root>
           \<SDKName>
                 \<SDKVersion>
                        SDKManifest.xml
                        \References
                              \<config>
                                    \<arch>
                        \Redist
                              \<config>
                                    \<arch>
                        \DesignTime
                               \<config>
                                     \<arch>

```

1. \\<SDKName<SDKVersion：扩展 SDK 的名称和版本派生自 SDK 根路径中的相应 \> \\ \> 文件夹名称。 MSBuild此标识在磁盘上查找 SDK，Visual Studio"属性"窗口和"引用管理器"对话框中显示 **此** 标识。 

2. *References* 文件夹：包含 API 的二进制文件。 这些元数据Windows WinMD (或) 元数据。

3. *Redist* 文件夹：运行时/调试所需的文件，应打包为用户应用程序的一部分。 所有二进制文件都应放置在 *\redist<\\ config<\> \\ \> arch* 下，并且二进制文件名称应采用以下格式以确保唯一性 *：]* \<company> . \<product> . \<purpose> 。 \<extension><em>.例如，*Microsoft.Cpp.Build.dll。</em> 名称可能与其他 SDK 的文件名冲突的所有文件 (例如 javascript、css、pri、xaml、png 和 jpg 文件) 都应放置在<em>\redist \\<config \> \\<arch<\> \\ sdkname \> 下面，但与 \* XAML 控件关联的文件除外。这些文件应位于 *\redist \\<config<\> \\ 组件<\> \\ 下 \> \\ </em>。

4. *DesignTime* 文件夹：仅在预运行/调试时需要的文件，不应打包为用户应用程序的一部分。 这些可能是 XML 文档、库、标头、工具箱设计时二进制文件、MSBuild项目等。 任何供本机项目使用 SDK 都必须具有 *SDKName.props* 文件。 下面显示了此类文件的示例。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <ExecutablePath>C:\Temp\ExecutablePath;$(ExecutablePath)</ExecutablePath>
       <IncludePath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\CommonConfiguration\Neutral\include;$(IncludePath)</IncludePath>
       <AssemblyReferencePath>C:\Temp\AssemblyReferencePath;(AssemblyReferencePath)</AssemblyReferencePath>
       <LibraryPath>$(FrameworkSDKRoot)\..\v8.1\ExtensionSDKs\cppimagingsdk\1.0\DesignTime\Debug\ARM;$(LibraryPath)</LibraryPath>
       <SourcePath>C:\Temp\SourcePath\X64;$(SourcePath)</SourcePath>
       <ExcludePath>C:\Temp\ExcludePath\X64;$(ExcludePath)</ExcludePath>
       <_PropertySheetDisplayName>DevILSDK, 1.0</_PropertySheetDisplayName>
     </PropertyGroup>
   </Project>

   ```

    XML 引用文档与引用文件一起放置。 例如 *，\References \\<config \> \\<arch \>\sample.dll* 程序集的 XML 参考文档是 *\References \\<config \> \\<arch \>\sample.xml，* 而该文档的本地化版本是 *\References<\\ config<arch<\> \\ \> \\ \> locale\sample.xml。*

5. *配置* 文件夹：三个子文件夹 *：Debug、Retail* 和 *CommonConfiguration*。 SDK 作者可以在使用同一组 SDK 文件时，将文件放在 *CommonConfiguration* 下，而不考虑 SDK 使用者所针对的配置。

6. *体系结构* 文件夹：支持以下体系结构：x86、x64、ARM、neutral。 Win32 映射到 x86，AnyCPU 映射到非特定。

### <a name="sdkmanifestxml"></a>SDKManifest.xml

SDKManifest.xml *文件* 介绍了Visual Studio SDK 的使用方式。 以下是一个示例：

```
<FileList DisplayName = "My SDK"
          ProductFamilyName = "My SDKs"
          TargetFramework = ".NETCore, version=v4.5.1; .NETFramework, version=v4.5.1"
          MinVSVersion = "14.0"
          MaxPlatformVersion = "8.1"
          AppliesTo = "WindowsAppContainer + WindowsXAML"
          SupportPrefer32Bit = "True"
          SupportedArchitectures = "x86;x64;ARM"
          SupportsMultipleVersions = "Error"
          CopyRedistToSubDirectory = "."
          DependsOn = "SDKB, version=2.0"
          MoreInfo = "https://msdn.microsoft.com/MySDK">
  <File Reference = "MySDK.Sprint.winmd" Implementation = "XNASprintImpl.dll">
    <Registration Type = "Flipper" Implementation = "XNASprintFlipperImpl.dll" />
    <Registration Type = "Flexer" Implementation = "XNASprintFlexerImpl.dll" />
    <ToolboxItems VSCategory = "Toolbox.Default" />
  </File>
</FileList>
```

以下列表提供了文件的元素：

1. DisplayName：在引用管理器、解决方案资源管理器、对象浏览器和用户界面的其他位置中显示的值，Visual Studio。

2. ProductFamilyName：整个 SDK 产品名称。 例如 [!INCLUDE[winjs_long](../debugger/includes/winjs_long_md.md)] ，SDK 名为"Microsoft.WinJS.1.0"和"Microsoft.WinJS.2.0"，它们属于同一系列 SDK 系列产品"Microsoft.WinJS"。 此属性允许Visual Studio MSBuild建立该连接。 如果此属性不存在，则 SDK 名称用作产品系列名称。

3. FrameworkIdentity：指定一个或多个组件Windows依赖项。 此属性的值将放入使用应用的清单中。 此属性仅适用于Windows库。

4. TargetFramework：指定引用管理器和工具箱中可用的 SDK。 这是以分号分隔的目标框架名字对象列表，例如".NET Framework，version=v2.0;.NET Framework，版本=v4.5.1"。 如果指定了同一目标框架的几个版本，则引用管理器将使用最低指定版本进行筛选。 例如，如果 ".NET Framework，version=v2.0;.NET Framework version=v4.5.1"时，引用管理器将使用".NET Framework，version=v2.0"。 如果指定了特定的目标框架配置文件，则引用管理器将仅将该配置文件用于筛选目的。 例如，如果指定了"Silverlight， version=v4.0， profile=WindowsPhone"，则引用管理器仅筛选Windows Phone配置文件;面向完整 Silverlight 4.0 Framework 的项目在引用管理器中看不到 SDK。

5. MinVSVersion：最低Visual Studio版本。

6. MaxPlatformVerson：最大目标平台版本应该用于指定扩展 SDK 将不起作用的平台版本。 例如，Microsoft Visual C++运行时包 v11.0 应仅由Windows 8引用。 因此，Windows 8项目的 MaxPlatformVersion 为 8.0。 这意味着引用管理器会筛选出Microsoft Visual C++项目的运行时Windows 8.1包，MSBuild项目引用它 [!INCLUDE[win81](../debugger/includes/win81_md.md)] 时引发错误。 注意：从 开始支持此元素 [!INCLUDE[vs_dev12](../extensibility/includes/vs_dev12_md.md)] 。

7. AppliesTo：指定引用管理器中可用的 SDK，具体Visual Studio类型。 识别了九个值：WindowsAppContainer、VisualC、VB、CSharp、WindowsXAML、JavaScript、Managed 和 Native。 SDK 作者可以使用 和 ("+') ， ("&#124;") ，而不是 ("！") 运算符来精确指定应用于 SDK 的项目类型的范围。

    WindowsAppContainer 标识应用 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 的项目。

8. SupportPrefer32Bit：支持的值为"True"和"False"。 默认值为"True"。 如果值设置为"False"，MSBuild如果引用 SDK 的项目启用了 Prefer32Bit，则 (将返回项目)  (或桌面项目的警告。 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 有关 Prefer32Bit 的信息，请参阅生成页、Project[设计器 (C#) ](../ide/reference/build-page-project-designer-csharp.md)或 编译页、Project[设计器 (Visual Basic) 。 ](../ide/reference/compile-page-project-designer-visual-basic.md)

9. SupportedArchitectures：SDK 支持的体系结构的分号分隔列表。 MSBuild使用项目中的目标 SDK 体系结构，则会显示警告。 如果未指定此属性，则MSBuild显示此类警告。

10. SupportsMultipleVersions：如果此属性设置为"错误"或"**警告**"，MSBuild指示同一项目无法引用同一 SDK 系列的多个版本。 如果此属性不存在或设置为 **"允许**"，MSBuild不显示这种类型的错误或警告。

11. AppX：为磁盘上的 Windows组件库指定应用包的路径。 在本地调试期间，此值Windows组件的注册组件。 文件名的命名约定为 *\<Company> . . \<Product> . . \<Architecture> . \<Configuration> \<Version> 。appx*。 配置和体系结构在属性名称和属性值中是可选的（如果它们不适用于Windows库）。 此值仅适用于Windows库。

12. CopyRedistToSubDirectory：指定 *\redist* 文件夹下的文件应相对于应用包根目录复制的位置 (即创建应用包向导) 和运行时布局根目录中选择的包位置。 默认位置是应用包和 **F5** 布局的根。

13. DependsOn：SDK 标识列表，用于定义此 SDK 所依赖的 SDK。 此属性显示在引用管理器的详细信息窗格中。

14. MoreInfo：提供帮助和详细信息的网页的 URL。 此值在引用管理器右窗格中的"更多信息"链接中使用。

15. 注册类型：在应用清单中指定 WinMD 注册，并且对于具有对应实现 DLL 的本机 WinMD 是必需的。

16. 文件引用：仅为包含控件或本机 WinMD 的引用指定。 若要了解如何指定引用是否包含控件，请参阅 [下面的指定工具箱项](#ToolboxItems) 的位置。

## <a name="specify-the-location-of-toolbox-items"></a><a name="ToolboxItems"></a> 指定工具箱项的位置

SDKManifest.xml架构的 **ToolBoxItems** *元素* 指定平台和扩展 SDK 中工具箱项的控件名称、源程序集和工具箱选项卡名称。 以下示例显示了各种方案。 这适用于 WinMD 或 DLL 引用。

请注意，在 Visual Studio 2019 及更早版本，Visual Studio SDK 程序集中动态枚举控件类型，而不是在清单中列出工具箱控件名称。 从 2022 Visual Studio开始，不再支持此功能;工具箱项必须显式列在 *SDKManifest.xml。*

1. 将控件放在工具箱的默认类别中。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Toolbox.Default">
        <Item Type = "Namespace.ControlName1" />
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

2. 将控件放在特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory= "MyCategoryName">
        <Item Type = "Namespace.ControlName1" />
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

3. 将控件放在特定类别名称下。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Graph">
        <Item Type = "Namespace.ControlName1" />
      </ToolboxItems>
      <ToolboxItems VSCategory = "Data">
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

4. 将控件放在 Blend 和 Visual Studio 中的不同类别名称下。

    ```xml
    // Blend accepts a slightly different structure for the category name because it allows a path rather than a single category.
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Graph" BlendCategory = "Controls/sample/Graph">
        <Item Type = "Namespace.ControlName1" />
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

5. 在 Blend 和 Visual Studio 中以不同方式枚举特定Visual Studio。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Graph">
        <Item Type = "Namespace.ControlName1" />
      </ToolboxItems>
      <ToolboxItems BlendCategory = "Controls/sample/Graph">
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

6. 枚举特定控件，将它们放在公共路径Visual Studio或仅放在"所有控件"组中。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Toolbox.Common">
        <Item Type = "Namespace.ControlName1" />
      </ToolboxItems>
      <ToolboxItems VSCategory = "Toolbox.All">
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

7. 枚举特定控件，并且仅在 ChooseItems 中显示特定集，而不在工具箱中显示它们。

    ```xml
    <File Reference = "sample.winmd">
      <ToolboxItems VSCategory = "Toolbox.ChooseItemsOnly">
        <Item Type = "Namespace.ControlName1" />
        <Item Type = "Namespace.ControlName2" />
      </ToolboxItems>
    </File>
    ```

## <a name="see-also"></a>另请参阅

- [演练：使用 C++ 创建 SDK](../extensibility/walkthrough-creating-an-sdk-using-cpp.md)
- [演练：使用 C# 或 Visual Basic](../extensibility/walkthrough-creating-an-sdk-using-csharp-or-visual-basic.md)
- [管理项目中的引用](../ide/managing-references-in-a-project.md)
