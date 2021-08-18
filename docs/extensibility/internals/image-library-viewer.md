---
title: 图像库查看器 |Microsoft Docs
description: 了解 Visual Studio 的图像库查看器工具，该工具可以加载和搜索图像清单，使您可以查看和操作图像属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 9d9c7fbb-ebae-4b20-9dd8-3c9070c0d0d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ee92f235bc973d0929e89ceae8d24f8ca77b9865
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122042369"
---
# <a name="image-library-viewer"></a>图像库查看器
Visual Studio 图像库查看器工具可以加载和搜索图像清单，使用户能够以相同的方式处理它们 Visual Studio。 用户可以更改背景、大小、DPI、高对比度和其他设置。 该工具还显示每个映像清单的加载信息，并显示映像清单中每个映像的源信息。 此工具适用于：

1. 诊断错误

2. 确保在自定义映像清单中正确设置属性

3. 在 Visual Studio 映像目录中搜索图像，使 Visual Studio 扩展可以使用适合的样式的图像 Visual Studio

   ![图像库查看器 Hero](../../extensibility/internals/media/image-library-viewer-hero.png "图像库查看器 Hero")

   **图像名字对象**

   简短) 的图像名字对象 (或名字对象是一个 GUID： ID 对，用于在映像库中唯一标识图像资产或图像列表资产。

   **映像清单文件**

   图像清单 (。 imagemanifest) 文件是 XML 文件，用于定义一组图像资产、表示这些资产的名字对象以及表示每个资产的真实图像或图像。 图像清单可以为旧版 UI 支持定义单独的图像或图像列表。 此外，还可以在资产上或每个资产后面的单个图像上设置属性，更改这些资产的显示时间和方式。

   **映像清单架构**

   完整的映像清单如下所示：

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Guid, ID, or String elements -->
      </Symbols>
      <!-- zero or one Images elements -->
      <Images>
        <!-- zero or more Image elements -->
      </Images>
      <!-- zero or one ImageLists elements -->
      <ImageLists>
        <!-- zero or more ImageList elements -->
      </ImageLists>
</ImageManifest>
```

 **符号**

 作为可读性和维护帮助，图像清单可以使用符号作为属性值。 符号定义如下：

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|**子元素**|**定义**|
|-|-|
|导入|导入给定清单文件的符号，以便在当前清单中使用。|
|Guid|符号表示 GUID 并且必须与 GUID 格式匹配。|
|ID|符号表示 ID，必须为非负整数。|
|字符串|符号表示任意字符串值。|

 符号区分大小写，并使用 $ (符号名) 语法进行引用：

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 某些符号是为所有清单预定义的。 它们可在或元素的 Uri 特性中使用 \<Source> \<Import> ，以引用本地计算机上的路径。

|**符号**|**说明**|
|-|-|
|CommonProgramFiles|% CommonProgramFiles% 环境变量的值|
|LocalAppData|% LocalAppData% 环境变量的值|
|ManifestFolder|包含清单文件的文件夹|
|MyDocuments|当前用户的 "我的文档" 文件夹的完整路径|
|ProgramFiles|% ProgramFiles% 环境变量的值|
|系统|Windows \System32 文件夹|
|WinDir|% WinDir% 环境变量的值|

 **图像**

 \<Image>元素定义可由名字对象引用的图像。 同时占用图像名字对象的 GUID 和 ID。 映像的名字对象在整个图像库中必须是唯一的。 如果有多个映像具有给定名字对象，则在生成库时遇到的第一个映像是保留的映像。

 它必须至少包含一个源。 虽然非特定大小的源将在各种大小范围内提供最佳结果，但它们并不是必需的。 如果请求服务的映像的大小未在元素中定义 \<Image> ，并且没有大小中立的源，则该服务将选择最佳的大小特定源，并将其缩放为请求的大小。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**Attribute**|**定义**|
|-|-|
|Guid|请求图像名字对象的 GUID 部分|
|ID|请求图像名字对象的 ID 部分|
|AllowColorInversion|[可选，默认值为 true]指示在深色背景上使用时，图像是否可以通过编程方式进行反转。|

 **Source**

 \<Source>元素定义单个图像源资产 (XAML 和 PNG) 。

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|**Attribute**|**定义**|
|-|-|
|Uri|请求一个 URI，用于定义图像的加载位置。 该参数可以是下列值之一：<br /><br /> -使用 application:///机构的[PACK URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf)<br /><br /> -绝对组件资源引用<br /><br /> -指向包含本机资源的文件的路径|
|背景|可有可无指示源要使用的背景类型。<br /><br /> 该参数可以是下列值之一：<br /><br /> - *浅*：源可在浅色背景上使用。<br /><br /> - *深色*：可在深色背景上使用源。<br /><br /> - *System.windows.forms.systeminformation.highcontrast*：源可在高对比度模式下的任何背景上使用。<br /><br /> - *HighContrastLight*：在高对比度模式下，可在浅色背景上使用源。<br /><br /> -*HighContrastDark*：在高对比度模式下，可以在深色背景上使用源。<br /><br /> 如果省略 **背景** 属性，则可以在任何背景上使用源。<br /><br /> 如果 **背景** 为 *浅*、 *暗*、 *HighContrastLight* 或 *HighContrastDark*，则源的颜色永远不会反转。 如果省略背景或将 **背景** 设置为 *system.windows.forms.systeminformation.highcontrast*，则源颜色的反转由图像的 **AllowColorInversion** 属性控制。|

 \<Source>元素可以具有以下一个可选子元素：

|**元素**|**属性 (所有必需的)**|**定义**|
|-|-|-|
|\<Size>|值|源将用于设备单位)  (给定大小的图像。 图像将为方形。|
|\<SizeRange>|MinSize，MaxSize|源将用于 MinSize 中的到 MaxSize (的图像，) 包括在内。 图像将为方形。|
|\<Dimensions>|Width, Height|源将用于以设备单位)  (给定的宽度和高度的图像。|
|\<DimensionRange>|MinWidth、MinHeight、<br /><br /> MaxWidth、MaxHeight|源将用于从最小宽度/高度到最大宽度/高度的图像，以设备单位 (（含) 为单位）。|

 \<Source>元素还可以具有可选的子元素，该子元素定义从本机程序集而不是托管程序集 \<NativeResource> \<Source> 加载的 。

```xml
<NativeResource Type="type" ID="int" />
```

|**Attribute**|**定义**|
|-|-|
|类型|[必需]本机资源的类型，XAML 或 PNG|
|ID|[必需]本机资源的整数 ID 部分|

 **ImageList**

 \<ImageList>元素定义可在单个条带中返回的图像集合。 根据需要按需生成条带。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**Attribute**|**定义**|
|-|-|
|Guid|[必需]图像名字对象的 GUID 部分|
|ID|[必需]图像名字对象的 ID 部分|
|外部|[可选，默认值为 false]指示映像名字对象是否引用当前清单中的映像。|

 包含映像的名字对象无需引用当前清单中定义的映像。 如果在图像库中找不到包含的图像，将在其位置使用空白占位符图像。

## <a name="how-to-use-the-tool"></a>如何使用工具
 **验证自定义映像清单**

 若要创建自定义清单，建议使用 ManifestFromResources 工具自动生成清单。 若要验证自定义清单，请启动图像库查看器并选择"文件">设置路径..."打开"搜索目录"对话框。 该工具将使用搜索目录来加载映像清单，但它还将使用它们查找清单中包含图像的 .dll 文件，因此请确保在此对话框中同时包含清单目录和 DLL 目录。

 ![图像库查看器 搜索](../../extensibility/internals/media/image-library-viewer-search.png "图像库查看器 搜索")

 单击 **"添加..."** 以选择新的搜索目录以搜索清单及其对应的 DLL。 该工具将记住这些搜索目录，并且可以通过检查或取消选中目录来打开或关闭这些目录。

 默认情况下，该工具将尝试查找Visual Studio目录，并将其添加到搜索目录列表。 可以手动添加工具找不到的目录。

 加载所有清单后，该工具可用于切换图像的背景色 **、DPI、** 高对比度或灰度缩放，以便用户可以直观地检查图像资产，以验证是否针对各种设置正确呈现图像资产。 

 ![图像库查看器 背景](../../extensibility/internals/media/image-library-viewer-background.png "图像库查看器 背景")

 背景色可以设置为浅色、深色或自定义值。 选择"自定义颜色"将打开颜色选择对话框，并添加该自定义颜色到背景组合框的底部，方便稍后进行召回。

 ![图像库查看器的自定义颜色](../../extensibility/internals/media/image-library-viewer-custom-color.png "图像库查看器的自定义颜色")

 选择图像名字对象会在右侧"图像详细信息"窗格中显示该名字对象后面的每个真实图像的信息。 该窗格还允许用户按名称或原始 GUID：ID 值复制名字对象。

 ![图像库查看器 图像详细信息](../../extensibility/internals/media/image-library-viewer-image-details.png "图像库查看器 图像详细信息")

 针对每个图像源显示的信息包括要显示的背景类型、是否可以将其作为颜色或支持 高对比度、其有效大小或大小是否与大小无关，以及图像是否来自本机程序集。

 ![图像库查看器 罐形主题](../../extensibility/internals/media/image-library-viewer-can-theme.png "图像库查看器 罐形主题")

 验证映像清单时，建议将清单和映像 DLL 部署到其实际位置。 这将验证任何相对路径是否正常工作，以及映像库是否可以找到并加载清单和映像 DLL。

 **搜索图像目录 KnownMonikers**

 为了更好地匹配Visual Studio样式，Visual Studio扩展可以使用映像目录中Visual Studio图像，而不是创建和使用自己的图像。 这样做的好处是无需维护这些图像，并且保证图像具有高 DPI 支持图像，因此，该图像在支持的所有 DPI 设置中Visual Studio正确。

 图像库查看器允许搜索清单，以便用户可以找到表示图像资产的名字对象，并使用该名字对象在代码中。 若要搜索图像，请在搜索框中输入所需的搜索词，然后按 Enter。 底部的状态栏将显示在所有清单中发现的图像总数中的匹配项数。

 ![图像库查看器 筛选器](../../extensibility/internals/media/image-library-viewer-filter.png "图像库查看器 筛选器")

 搜索现有清单中的图像名字对象时，建议仅搜索并使用 Visual Studio 映像目录的名字对象、其他有意公开访问的名字对象或你自己的自定义名字对象。 如果使用非公有名字对象，则当更改或更新这些非公有名字对象和图像时，自定义 UI 可能会损坏或意外更改其图像。

 此外，还可以按 GUID 进行搜索。 此类型的搜索可用于将列表向下筛选为单个清单，或将清单的单个子节筛选为包含多个 GUID 的清单。

 ![图像库查看器 筛选器 GUID](../../extensibility/internals/media/image-library-viewer-filter-guid.png "图像库查看器 筛选器 GUID")

 最后，也能够按 ID 进行搜索。

 ![图像库查看器 筛选器 ID](../../extensibility/internals/media/image-library-viewer-filter-id.png "图像库查看器 筛选器 ID")

## <a name="notes"></a>说明

- 默认情况下，该工具将拉取安装目录中Visual Studio清单。 只有 **Microsoft.VisualStudio.ImageCatalog** 清单具有可公开使用的名字对象。 GUID：ae27a6b0-e345-4288-96df-5eaf394ee369 (**请勿** 在自定义清单中重写此 GUID) 类型： KnownMonikers

- 该工具在启动时尝试加载找到的所有映像清单，因此应用程序可能需要几秒钟时间，应用程序实际显示。 加载清单时，它也可能很慢或无响应。

## <a name="sample-output"></a>示例输出
 此工具不生成任何输出。
