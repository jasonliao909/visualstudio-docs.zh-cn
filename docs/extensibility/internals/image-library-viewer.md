---
title: 图像库查看器|Microsoft Docs
description: 了解用于Visual Studio和搜索图像清单的映像库查看器工具，以便查看和操作图像属性。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664805"
---
# <a name="image-library-viewer"></a>图像库查看器
图像Visual Studio查看器工具可以加载和搜索图像清单，允许用户以与用户相同的方式Visual Studio清单。 用户可以更改背景、大小、DPI、高对比度和其他设置。 该工具还显示每个映像清单的加载信息，并显示映像清单中每个图像的源信息。 此工具可用于：

1. 诊断错误

2. 确保在自定义映像清单中正确设置属性

3. 在图像目录中Visual Studio图像，以便Visual Studio扩展可以使用适合图像样式Visual Studio

   ![图像库查看器 Hero](../../extensibility/internals/media/image-library-viewer-hero.png "图像库查看器 Hero")

   **图像名字对象**

   图像名字对象 (或名字对象) 是 GUID：ID 对，用于唯一标识图像库中的图像资产或图像列表资产。

   **映像清单文件**

   映像清单 (.imagemanifest) 文件是 XML 文件，用于定义一组图像资产、表示这些资产的名字对象以及代表每个资产的真实图像或图像。 映像清单可以定义独立映像或图像列表，以支持旧版 UI。 此外，还可以在资产上或每个资产后面的单个图像上设置属性，以更改显示这些资产时和方式。

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

 作为可读性和维护辅助，映像清单可以将符号用于属性值。 符号定义如下：

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
|导入|导入给定清单文件的符号，以用于当前清单。|
|Guid|符号表示 GUID，并且必须与 GUID 格式匹配。|
|ID|符号表示一个 ID，并且必须是非正整数。|
|字符串|符号表示任意字符串值。|

 符号区分大小写，使用 $ (符号名称) 语法引用：

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 某些符号已针对所有清单进行预定义。 这些可在 或 元素的 Uri \<Source> 属性 \<Import> 中用于引用本地计算机上的路径。

|**符号**|**描述**|
|-|-|
|CommonProgramFiles|%CommonProgramFiles% 环境变量的值|
|LocalAppData|%LocalAppData% 环境变量的值|
|ManifestFolder|包含清单文件的文件夹|
|MyDocuments|当前用户我的文档文件夹的完整路径|
|ProgramFiles|%ProgramFiles% 环境变量的值|
|系统|Windows\System32 文件夹|
|WinDir|%WinDir% 环境变量的值|

 **图像**

 \<Image>元素定义一个可通过名字对象引用的图像。 GUID 和 ID 共同构成了图像名字对象。 图像的名字对象在整个图像库中必须是唯一的。 如果多个映像具有给定的名字对象，则生成库时遇到的第一个映像是保留的映像。

 它必须包含至少一个源。 尽管与大小无关的源可跨各种大小提供最佳结果，但这不是必需的。 如果要求服务提供未在 元素中定义的大小的图像，并且没有与大小无关的源，则服务将选择特定于大小的最佳源，并缩放到 \<Image> 请求的大小。

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**Attribute**|**定义**|
|-|-|
|Guid|[必需]图像名字对象的 GUID 部分|
|ID|[必需]图像名字对象的 ID 部分|
|AllowColorInversion|[可选，默认为 true]指示在深色背景上使用图像时，是否可以以编程方式反转其颜色。|

 **Source**

 元素 \<Source> 定义 XAML 和 PNG (单个图像源) 。

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|**Attribute**|**定义**|
|-|-|
|Uri|[必需]一个 URI，用于定义可以从何处加载映像。 该参数可以是下列值之一：<br /><br /> - [使用证书](/dotnet/framework/wpf/app-development/pack-uris-in-wpf) 颁发机构 application:/// URI<br /><br /> - 绝对组件资源引用<br /><br /> - 包含本机资源的文件的路径|
|背景|[可选]指示源使用的背景类型。<br /><br /> 该参数可以是下列值之一：<br /><br /> - *浅* 色：源可用于浅色背景。<br /><br /> - *深色*：源可用于深色背景。<br /><br /> - *HighContrast：* 源可以在任何背景上用于高对比度模式。<br /><br /> - *HighContrastLight：* 源可以在光背景上用于高对比度模式。<br /><br /> -*HighContrastDark：* 源可以在深色背景上以高对比度使用。<br /><br /> 如果 **省略 Background** 属性，则源可用于任何背景。<br /><br /> 如果 **背景** 为 *浅* 色 *、* 深色、 *高ContrastLight* 或 *HighContrastDark，* 则源的颜色永远不会反转。 如果 **省略 Background** 或设置为 *HighContrast，* 则源颜色的反转由图像的 **AllowColorInversion** 属性控制。|

 元素 \<Source> 只能有以下可选子元素之一：

|**元素**|**属性 (所有必需的)**|**定义**|
|-|-|-|
|\<Size>|值|源将用于给定大小图像， (设备单位) 。 图像将为正方形。|
|\<SizeRange>|MinSize、MaxSize|源将用于从 MinSize 到 MaxSize (设备单位（含) 图像）。 图像将为正方形。|
|\<Dimensions>|Width, Height|源将用于给定宽度和高度的图像， (设备单位) 。|
|\<DimensionRange>|MinWidth、MinHeight、<br /><br /> System.windows.frameworkelement.maxwidth、System.windows.frameworkelement.maxheight|源将用于从最小宽度/高度到最大宽度/高度的图像 (以设备单位) 表示。|

 \<Source>元素还可以具有可选的 \<NativeResource> 子元素，此子元素定义 \<Source> 从本机程序集而不是托管程序集加载的。

```xml
<NativeResource Type="type" ID="int" />
```

|**Attribute**|**定义**|
|-|-|
|类型|请求本机资源的类型（XAML 或 PNG）|
|ID|请求本机资源的整数 ID 部分|

 **ImageList**

 \<ImageList>元素定义可在单个条带中返回的图像集合。 根据需要，可按需生成条带。

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**Attribute**|**定义**|
|-|-|
|Guid|请求图像名字对象的 GUID 部分|
|ID|请求图像名字对象的 ID 部分|
|外部|[可选，默认值为 false]指示图像名字对象是否引用当前清单中的图像。|

 包含的图像的名字对象不必引用在当前清单中定义的映像。 如果在图像库中找不到包含的图像，则会在其位置使用空白占位符图像。

## <a name="how-to-use-the-tool"></a>如何使用该工具
 **验证自定义映像清单**

 若要创建自定义清单，建议使用 ManifestFromResources 工具来自动生成清单。 若要验证自定义清单，请启动图像库查看器并选择 "文件" > "设置路径 ..."打开 "搜索目录" 对话框。 该工具将使用搜索目录加载图像清单，但它还会将其用于查找包含清单中的图像的 .dll 文件，因此请确保在此对话框中包含清单和 DLL 目录。

 ![图像库查看器 搜索](../../extensibility/internals/media/image-library-viewer-search.png "图像库查看器 搜索")

 单击 " **添加 ...** " 选择新的搜索目录，搜索清单及其相应的 dll。 该工具将记住这些搜索目录，并且可以通过选中或取消选中某个目录来打开或关闭它们。

 默认情况下，该工具将尝试查找 Visual Studio 安装目录，并将这些目录添加到搜索目录列表中。 您可以手动添加该工具找不到的目录。

 加载所有清单后，可以使用该工具切换图像的 **背景** 色、 **DPI**、 **高对比度** 或 **grayscaling** ，以便用户可以通过视觉方式检查图像资产，以验证它们是否能正确地针对各种设置进行呈现。

 ![图像库查看器 背景](../../extensibility/internals/media/image-library-viewer-background.png "图像库查看器 背景")

 可以将背景色设置为 "浅"、"深" 或 "自定义" 值。 选择 "自定义颜色" 将打开颜色选择对话框，并将该自定义颜色添加到 "背景" 组合框的底部，以便稍后重新调用。

 ![图像库查看器的自定义颜色](../../extensibility/internals/media/image-library-viewer-custom-color.png "图像库查看器的自定义颜色")

 选择图像名字对象将在右侧的 "图像详细信息" 窗格中显示该名字对象后面的每个真实图像的信息。 该窗格还允许用户按名称或原始 GUID： ID 值复制名字对象。

 ![图像库查看器 图像详细信息](../../extensibility/internals/media/image-library-viewer-image-details.png "图像库查看器 图像详细信息")

 为每个图像源显示的信息包括要在其上显示的背景类型、是否可以主题或支持高对比度、其有效大小或是否为非特定大小，以及图像是否来自本机程序集。

 ![图像库查看器 罐形主题](../../extensibility/internals/media/image-library-viewer-can-theme.png "图像库查看器 罐形主题")

 在验证映像清单时，建议您在实际的位置部署清单和映像 DLL。 这将验证任何相对路径是否正常工作，以及图像库是否可以查找并加载清单和映像 DLL。

 **搜索 image catalog KnownMonikers**

 为了更好地匹配 Visual Studio 样式，Visual Studio 扩展可以使用 Visual Studio 映像目录中的图像，而不是创建和使用自己的映像。 这样做的好处是不必维护这些映像，并保证映像具有高 DPI 后备图像，使其在 Visual Studio 支持的所有 DPI 设置中正确显示。

 图像库查看器允许搜索清单，以便用户可以查找表示图像资产的名字对象并在代码中使用该名字对象。 若要搜索图像，请在搜索框中输入所需的搜索词，然后按 Enter。 底部的状态栏将显示从所有清单中的映像总数中发现了多少个匹配项。

 ![图像库查看器 筛选器](../../extensibility/internals/media/image-library-viewer-filter.png "图像库查看器 筛选器")

 在现有清单中搜索图像名字对象时，建议仅搜索并使用 Visual Studio 映像目录的名字对象、其他有意公开访问的名字对象或您自己的自定义名字对象。 如果使用非公共名字对象，则自定义 UI 可能会损坏，或者在更改或更新这些非公共名字对象和图像时以意外的方式更改其图像。

 此外，还可以按 GUID 进行搜索。 这种类型的搜索可用于将列表筛选到单个清单或清单中的单个子节（如果该清单包含多个 Guid）。

 ![图像库查看器 筛选器 GUID](../../extensibility/internals/media/image-library-viewer-filter-guid.png "图像库查看器 筛选器 GUID")

 最后，还可以按 ID 进行搜索。

 ![图像库查看器 筛选器 ID](../../extensibility/internals/media/image-library-viewer-filter-id.png "图像库查看器 筛选器 ID")

## <a name="notes"></a>说明

- 默认情况下，该工具会提取 Visual Studio 安装目录中的多个映像清单。 只有一个具有公开的名字对象的是 **VisualStudio. ImageCatalog** 清单。 GUID： ae27a6b0-e345-4288-96df-5eaf394ee369 (不要在自定义清单 **中重写** 此 GUID) 类型： KnownMonikers

- 该工具在启动时尝试加载它找到的所有映像清单，因此应用程序可能需要几秒钟才能实际显示。 加载清单时，它可能会变慢或无响应。

## <a name="sample-output"></a>示例输出
 此工具不会生成任何输出。
