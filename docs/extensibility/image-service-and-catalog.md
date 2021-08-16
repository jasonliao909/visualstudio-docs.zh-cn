---
title: 映像服务和目录|Microsoft Docs
description: 本文包含采用映像服务和映像目录Visual Studio指南和最佳做法。
ms.custom: SEO-VS-2020
ms.date: 04/01/2019
ms.topic: conceptual
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: a2967f2d29b07a574856810cb113ab5523a0484aa33644b1796548f40aa05018
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432648"
---
# <a name="image-service-and-catalog"></a>映像服务和目录
本指南包含有关采用 2015 年 1 月Visual Studio中引入的映像服务和映像目录的指南Visual Studio最佳做法。

 2015 Visual Studio 中引入的图像服务使开发人员能够获取设备的最佳图像和用户选择的主题来显示图像，包括针对显示图像的上下文更正主题。 采用映像服务有助于消除与资产维护、HDPI 缩放和主题相关的主要问题。

|**当前问题**|**解决方案**|
|-|-|
|背景色混合|内置 alpha 混合|
|对一 (图像进行) |主题元数据|
|高对比度模式|备用高对比度资源|
|需要多个资源用于不同的 DPI 模式|具有基于矢量的回退的可选择资源|
|复制图像|每个图像概念一个标识符|

 为什么要采用映像服务？

- 始终从图像获取最新的"像素完美"Visual Studio

- 可以提交并使用自己的映像

- 添加新 DPI 缩放时，无需Windows图像

- 解决实现中的旧体系结构障碍

  使用Visual Studio之前和之后，shell 工具栏：

  ![图像服务前后对比](../extensibility/media/image-service-before-and-after.png "图像服务前后对比")

## <a name="how-it-works"></a>工作原理
 图像服务可以提供适用于任何受支持的 UI 框架的位图映像：

- WPF：BitmapSource

- WinForms：System.Drawing.Bitmap

- Win32：HBITMAP

  图像服务流程图

  ![图像服务流关系图](../extensibility/media/image-service-flow-diagram.png "图像服务流关系图")

  **图像名字对象**

  图像名字对象 (或名字对象) 是一个 GUID/ID 对，用于唯一标识映像库中的图像资产或图像列表资产。

  **已知名字对象**

  映像目录中包含的图像名字对象Visual Studio，由任何映像组件或扩展Visual Studio公开使用。

  **映像清单文件**

  映像 (*.imagemanifest*) 文件是 XML 文件，用于定义一组图像资产、表示这些资产的名字对象，以及代表每个资产的真实图像或图像。 映像清单可以定义独立映像或图像列表，以支持旧版 UI。 此外，还可以在资产上或每个资产后面的单个图像上设置属性，以更改显示这些资产时和方式。

  **映像清单架构**

  完整的映像清单如下所示：

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Import, Guid, ID, or String elements -->
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
|导入|导入给定清单文件的符号，以用于当前清单|
|Guid|符号表示 GUID，必须与 GUID 格式匹配|
|ID|符号表示 ID，并且必须是非空整数|
|String|符号表示任意字符串值|

 符号区分大小写，使用 $ (符号名称) 语法引用：

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 某些符号已针对所有清单进行预定义。 这些可在 或 元素的 Uri \<Source> 属性 \<Import> 中用于引用本地计算机上的路径。

|**符号**|**说明**|
|-|-|
|CommonProgramFiles|%CommonProgramFiles% 环境变量的值|
|LocalAppData|%LocalAppData% 环境变量的值|
|ManifestFolder|包含清单文件的文件夹|
|MyDocuments|当前用户我的文档文件夹的完整路径|
|ProgramFiles|%ProgramFiles% 环境变量的值|
|系统|*Windows\System32* 文件夹|
|WinDir|%WinDir% 环境变量的值|

 **图像**

 \<Image>元素定义一个可通过名字对象引用的图像。 GUID 和 ID 共同构成了图像名字对象。 图像的名字对象在整个图像库中必须是唯一的。 如果多个映像具有给定的名字对象，则生成库时遇到的第一个映像是保留的映像。

 它必须包含至少一个源。 非特定大小的源可跨各种大小提供最佳结果，但这不是必需的。 如果要求服务提供未在 元素中定义的大小的图像，并且没有与大小无关的源，则服务将选择特定于大小的最佳源，并缩放到 \<Image> 请求的大小。

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
|Uri|[必需]一个 URI，用于定义可以从何处加载映像。 该参数可以是下列值之一：<br /><br /> - [使用证书](/dotnet/framework/wpf/app-development/pack-uris-in-wpf) 颁发机构 application:/// URI<br />- 绝对组件资源引用<br />- 包含本机资源的文件的路径|
|背景|[可选]指示源使用的背景类型。<br /><br /> 该参数可以是下列值之一：<br /><br /> *浅色：* 源可用于浅色背景。<br /><br /> *深色：* 源可用于深色背景。<br /><br /> *HighContrast：* 源可以在任何背景上用于高对比度模式。<br /><br /> *HighContrastLight：* 源可以在浅色背景上以高对比度模式使用。<br /><br /> *HighContrastDark：* 源可以在深色背景上以高对比度使用。<br /><br /> 如果省略 Background 属性，则源可用于任何背景。<br /><br /> 如果背景为 *浅* 色 *、* 深色、 *高ContrastLight* 或 *HighContrastDark，* 则源的颜色永远不会反转。 如果省略 Background 或设置为 *HighContrast，* 则源颜色的反转由图像的 **AllowColorInversion** 属性控制。|

元素 \<Source> 只能有以下可选子元素之一：

|**元素**|**属性 (所有必需的)**|**定义**|
|-|-|-|
|\<Size>|值|源将用于给定大小图像（ (设备单位) 。 图像将为正方形。|
|\<SizeRange>|MinSize、MaxSize|源将用于从 MinSize 到 MaxSize (设备单位（含) 图像）。 图像将为正方形。|
|\<Dimensions>|Width, Height|源将用于给定宽度和高度的图像， (设备单位) 。|
|\<DimensionRange>|MinWidth、MinHeight、<br /><br /> MaxWidth、MaxHeight|源将用于从最小宽度/高度到最大宽度/高度（以设备单位为单位 (（含) ）的图像。|

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

## <a name="using-the-image-service"></a>使用映像服务

### <a name="first-steps-managed"></a>托管 (步骤) 
 若要使用映像服务，需要向项目添加对以下部分或所有程序集的引用：

- *Microsoft.VisualStudio.ImageCatalog.dll*

  - 如果使用内置映像目录 **KnownMonikers**，是必需的。

- *Microsoft.VisualStudio.Imaging.dll*

  - 如果在 WPF UI 中使用 **CrispImage** 和 **ImageThemingUtilities，** 是必需的。

- *Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll*

  - 如果使用 **ImageMoniker 和** **ImageAttributes 类型，是必需的** 。

  - **EmbedInteropTypes** 应设置为 true。

- *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime*

  - 如果使用 **IVsImageService2 类型，是必需的** 。

  - **EmbedInteropTypes** 应设置为 true。

- *Microsoft.VisualStudio.Utilities.dll*

  - 如果在 WPF UI 中对 **ImageThemingUtilities.ImageBackgroundColor** 使用 **BrushToColorConverter，** 是必需的。

- *Microsoft.VisualStudio.Shell。 \<VSVersion>0*

  - 如果使用 **IVsUIObject 类型，** 是必需的。

- *Microsoft.VisualStudio.Shell.Interop.10.0.dll*

  - 如果使用与 WinForms 相关的 UI 帮助程序，是必需的。

  - **EmbedInteropTypes** 应设置为 true

### <a name="first-steps-native"></a>本机 (步骤) 
 若要使用映像服务，需要将以下部分或所有标头包含到项目中：

- **KnownImageIds.h**

  - 如果使用内置映像目录 **KnownMonikers，** 但无法使用 **ImageMoniker** 类型（例如从 **IVsHierarchy GetGuidProperty** 或 **GetProperty** 调用返回值时，则是必需的）。

- **KnownMonikers.h**

  - 如果使用内置映像目录 **KnownMonikers**，是必需的。

- **ImageParameters140.h**

  - 如果使用 **ImageMoniker 和** **ImageAttributes 类型，是必需的** 。

- **VSShell140.h**

  - 如果使用 **IVsImageService2 类型，是必需的** 。

- **ImageThemingUtilities.h**

  - 如果无法让映像服务处理它们，则是必需的。

  - 如果映像服务可以处理映像标题，请不要使用此标头。

::: moniker range="vs-2017"
- **VSUIDPIHelper.h**

  - 如果使用 DPI 帮助程序获取当前 DPI，是必需的。

::: moniker-end

::: moniker range=">=vs-2019"
- **VsDpiAwareness.h**

  - 如果使用 DPI 感知帮助程序获取当前 DPI，是必需的。

::: moniker-end

## <a name="how-do-i-write-new-wpf-ui"></a>如何实现编写新的 WPF UI？

1. 首先，将上述步骤部分所需的程序集引用添加到项目。 不需要添加所有这些引用，因此只需添加所需的引用。  (注意：如果使用 或 有权访问 **Colors** 而不是 **画笔**，则你可以跳过对实用工具 的引用，因为不需要converter.) 

2. 选择所需的图像并获取其名字对象。 使用 **KnownMoniker**，如果具有自己的自定义映像和名字对象，请使用自己的 。

3. 将 **CrispImages** 添加到 XAML。  (请参阅以下示例.) 

4. 在 UI **层次结构中设置 ImageThemingUtilities.ImageBackgroundColor** 属性。  (应在背景色已知的位置设置此设置，不一定在 **"CrispImage"** 上设置)  (请参阅以下示例.) 

```xaml
<Window
  x:Class="WpfApplication.MainWindow"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:imaging="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:theming="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:utilities="clr-namespace:Microsoft.Internal.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:catalog="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.ImageCatalog"
  Title="MainWindow" Height="350" Width="525" UseLayoutRounding="True">
  <Window.Resources>
    <utilities:BrushToColorConverter x:Key="BrushToColorConverter"/>
  </Window.Resources>
  <StackPanel Background="White" VerticalAlignment="Center"
    theming:ImageThemingUtilities.ImageBackgroundColor="{Binding Background, RelativeSource={RelativeSource Self}, Converter={StaticResource BrushToColorConverter}}">
    <imaging:CrispImage Width="16" Height="16" Moniker="{x:Static catalog:KnownMonikers.MoveUp}" />
  </StackPanel>
</Window>
```

 **如何实现现有的 WPF UI？**

 更新现有的 WPF UI 是一个相对简单的过程，由三个基本步骤组成：

1. 将 \<Image> UI 中所有元素替换为 \<CrispImage> 元素。

2. 将所有源属性更改为名字对象属性。

    - 如果映像永远不会更改，并且你使用的是 **KnownMonikers，** 则以静态方式将该属性绑定到 **KnownMoniker**。  (请参阅上面的示例.) 

    - 如果映像永远不会更改，并且使用的是自己的自定义映像，则静态绑定到自己的名字对象。

    - 如果图像可更改，请将名字对象特性绑定到在属性更改时发出通知的代码属性。

3. 在 UI 层次结构中的某个位置，将 **ImageThemingUtilities** 设置为确保颜色反转正确工作。

    - 这可能需要使用 **BrushToColorConverter** 类。  (参见上面的示例。 ) 

## <a name="how-do-i-update-win32-ui"></a>如何实现更新 Win32 UI？
 将以下代码添加到代码中的任意位置，以替换映像的原始加载。 根据需要切换值以返回 HBITMAPs 与 HICONs 与 HIMAGELIST。

 **获取映像服务**

```cpp
CComPtr<IVsImageService2> spImgSvc;
CGlobalServiceProvider::HrQueryService(SID_SVsImageService, &spImgSvc);
```

 **请求映像**

::: moniker range="vs-2017"

```cpp
ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = VsUI::DpiHelper::GetDeviceDpiX();
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

::: moniker range=">=vs-2019"

```cpp
UINT dpiX, dpiY;
HWND hwnd = // get the HWND where the image will be displayed
VsUI::CDpiAwareness::GetDpiForWindow(hwnd, &dpiX, &dpiY);

ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = dpiX;
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

## <a name="how-do-i-update-winforms-ui"></a>如何实现更新 WinForms UI？
 将以下代码添加到代码中的任意位置，以替换映像的原始加载。 根据需要切换返回位图和图标的值。

 **有用的 using 语句**

```csharp
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;
```

 **获取映像服务**

```csharp
// This or your preferred way of querying for Visual Studio services
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));

```

 **请求映像**

::: moniker range="vs-2017"

```csharp
ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiHelper.DeviceDpiX;
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

::: moniker range=">=vs-2019"

```csharp
Control control = // get the control where the image will be displayed

ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiAwareness.GetWindowDpi(control.Handle);
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>如何实现在新的工具窗口中使用图像名字对象？
 已更新 Visual Studio 2015 的 VSIX 包项目模板。 若要创建新的工具窗口，请右键单击 VSIX 项目，然后选择 "**添加**  >  **新项**" (**Ctrl** + **Shift** + **a**) 。 在项目语言的 "扩展性" 节点下，选择 " **自定义工具窗口**"，为工具窗口提供一个名称，然后按 " **添加** " 按钮。

 这些是在工具窗口中使用名字对象的关键位置。 按照以下各项的说明操作：

1. 当选项卡变小时，"工具窗口" 选项卡 (也可用于 " **Ctrl** + **" 选项卡** 窗口切换器) 。

    将以下行添加到从 **ToolWindowPane** 类型派生的类的构造函数：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   this.BitmapImageMoniker = KnownMonikers.Blank;
   ```

2. 用于打开工具窗口的命令。

    在包的 *.vsct* 文件中，编辑工具窗口的命令按钮：

   ```xml
   <Button guid="guidPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <!-- Replace this KnownMoniker with your desired ImageMoniker -->
     <Icon guid="ImageCatalogGuid" id="Blank" />
     <!-- Add this -->
     <CommandFlag>IconIsMoniker</CommandFlag>
     <Strings>
       <ButtonText>MyToolWindow</ButtonText>
     </Strings>
   </Button>
   ```

   **如何实现在现有工具窗口中使用图像名字对象？**

   更新现有工具窗口以使用映像名字对象类似于创建新工具窗口的步骤。

   这些是在工具窗口中使用名字对象的关键位置。 按照以下各项的说明操作：

3. 当选项卡变小时，"工具窗口" 选项卡 (也可用于 " **Ctrl** + **" 选项卡** 窗口切换器) 。

   1. 如果这些行) 存在于从 **ToolWindowPane** 类型派生的类的构造函数中，则删除这些行 (：

       ```csharp
       this.BitmapResourceID = <Value>;
       this.BitmapIndex = <Value>;
       ```

   2. 请参阅 "如何实现在新工具窗口中使用图像名字对象" 的步骤 #1。 一节。

4. 用于打开工具窗口的命令。

   - 请参阅 "如何实现在新工具窗口中使用图像名字对象" 的步骤 #2。 一节。

## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>如何实现使用 .vsct 文件中的图像名字对象？
 按照下面的注释行所示更新 *.vsct* 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!--  Include the definitions for images included in the VS image catalog -->
  <Include href="KnownImageIds.vsct"/>
  <Commands package="guidMyPackage">
    <Buttons>
      <Button guid="guidMyCommandSet" id="cmdidMyCommand" priority="0x0000" type="Button">
        <!-- Add an Icon element, changing the attributes to match the image moniker you want to use.
             In this case, we're using the Guid for the VS image catalog.
             Change the id attribute to be the ID of the desired image moniker. -->
        <Icon guid="ImageCatalogGuid" id="OpenFolder" />
        <CommandFlag>DynamicVisibility</CommandFlag>
        <CommandFlag>DefaultInvisible</CommandFlag>
        <CommandFlag>DefaultDisabled</CommandFlag>
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>IconAndText</CommandFlag>
        <!-- Add the IconIsMoniker CommandFlag -->
        <CommandFlag>IconIsMoniker</CommandFlag>
        <Strings>
          <ButtonText>Quick Fixes...</ButtonText>
          <CommandName>Show Quick Fixes</CommandName>
          <CanonicalName>ShowQuickFixes</CanonicalName>
          <LocCanonicalName>ShowQuickFixes</LocCanonicalName>
        </Strings>
      </Button>
    </Buttons>
  </Commands>
  <!-- It is recommended that you remove <Bitmap> elements that are no longer used in the vsct file -->
  <Symbols>
    <GuidSymbol name="guidMyPackage"    value="{1491e936-6ffe-474e-8371-30e5920d8fdd}" />
    <GuidSymbol name="guidMyCommandSet" value="{10347de4-69a9-47f4-a950-d3301f6d2bc7}">
      <IDSymbol name="cmdidMyCommand" value="0x9437" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```

 **如果旧版本的 Visual Studio 需要读取 .vsct 文件怎么办？**

 旧版本的 Visual Studio 不能识别 **IconIsMoniker** 命令标志。 可以在支持的 Visual Studio 版本的映像服务中使用映像，但会继续在旧版本的 Visual Studio 上使用旧样式的映像。 若要执行此操作，请将 *.vsct* 文件保持不变 (并因此与 Visual Studio) 的旧版本兼容，并创建 CSV (逗号分隔值) 文件，该文件从 *.vsct* 文件的元素中定义的 guid/id 对映射 \<Bitmaps> 到映像名字对象 GUID/id 对。

 映射 CSV 文件的格式为：

```
Icon guid, Icon id, Moniker guid, Moniker id
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200
```

 CSV 文件随包一起部署，其位置由 **ProvideMenuResource** 包特性的 **IconMappingFilename** 属性指定：

```csharp
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]
```

 **IconMappingFilename** 是隐式地以 $PackageFolder $ (（如上面的示例所示）) 的相对路径，或者是以环境变量（如 *@ "% UserProfile% \dir1\dir2\MyMappingFile.csv"*）定义的目录的绝对路径。

## <a name="how-do-i-port-a-project-system"></a>如何实现移植项目系统？
 **如何为项目提供 ImageMonikers**

1. 在项目的 **IVsHierarchy** 上实现 **VSHPROPID_SupportsIconMonikers** ，并返回 true。

2. 如果原始项目 **使用的是** **VSHPROPID_IconImgList**) 或 **VSHPROPID_IconMonikerGuid**，则实现 **VSHPROPID_IconMonikerImageList** (如果原始项目使用 **VSHPROPID_IconMonikerId** 和 **VSHPROPID_OpenFolderIconMonikerGuid** VSHPROPID_OpenFolderIconMonikerId (**VSHPROPID_IconHandle VSHPROPID_OpenFolderIconHandle)** 。

3. 更改原始 VSHPROPIDs 的图标的实现，以便在扩展点请求时创建图标的 "旧" 版本。 **IVsImageService2** 提供了获取这些图标所需的功能

   **VB/C # 项目风格的额外要求**

   如果检测到你的项目是 **最外面的风格**，则仅实现 **VSHPROPID_SupportsIconMonikers** 。 否则，实际最外面的风格可能不支持图像名字对象，因此，你的基础风格可能会有效地 "隐藏" 自定义图像。

   **如何实现使用 CPS 中的映像名字对象？**

   在 CPS 中设置自定义映像 (常见 Project 系统) 可以手动完成，也可以通过 Project 系统扩展性 SDK 随附的项模板来完成。

   **使用 Project 系统扩展性 SDK**

   按照为[Project 类型/项类型提供自定义图标](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md)中的说明自定义 CPS 映像。 有关 CPS 的详细信息，请参阅[Visual Studio Project 系统扩展性文档](https://github.com/Microsoft/VSProjectSystem)

   **手动使用 ImageMonikers**

4. 实现和导出项目系统中的 **IProjectTreeModifier** 接口。

5. 确定要使用的 **KnownMoniker** 或自定义映像名字对象。

6. 在 **ApplyModifications** 方法中，在方法中的某处执行以下操作，然后返回新树，类似于下面的示例：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());
   ```

7. 如果要创建新树，可以通过将所需的名字对象传入 NewTree 方法来设置自定义映像，类似于以下示例：

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   ProjectImageMoniker icon         = KnownMonikers.FolderClosed.ToProjectSystemType();
   ProjectImageMoniker expandedIcon = KnownMonikers.FolderOpened.ToProjectSystemType();

   return this.ProjectTreeFactory.Value.NewTree(/*caption*/<value>,
                                                /*filePath*/<value>,
                                                /*browseObjectProperties*/<value>,
                                                icon,
                                                expandedIcon);
   ```

## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>如何实现从真实图像条转换为基于名字对象的图像条？
 **我需要支持 HIMAGELISTs**

 如果你要更新的代码有一个现有的图像条以使用映像服务，但你受需要通过图像列表传递的 Api 的约束，则仍可获得映像服务的优势。 若要创建基于名字对象的图像条，请按照以下步骤从现有名字对象创建清单。

1. 运行 **ManifestFromResources** 工具，并向其传递图像条。 这将为条带生成清单。

   - 建议：提供清单的非默认名称，以适合其使用情况。

2. 如果仅使用 **KnownMonikers**，请执行以下操作：

   - \<Images>将清单的部分替换为 \<Images/> 。

   - 删除所有 subimage Id (带有 \<imagestrip name> _ # # ) 的所有 id。

   - 建议：重命名 AssetsGuid 符号和图像条符号以适应其用法。

   - 将每个 **ContainedImage** 的 GUID 替换为 $ (ImageCatalogGuid) ，将每个 **ContainedImage** 的 ID 替换为 $ (\<moniker>) ，并向每个 **ContainedImage** 添加 External = "true" 属性。

       - \<moniker> 应该替换为与图像匹配但带有 "KnownMonikers" 的 **KnownMoniker** 。 从名称中删除。

   - 添加 <Import Manifest = "$ (ManifestFolder) \\<相对安装目录路径到 * \> \Microsoft.VisualStudio.ImageCatalog.imagemanifest"/ \*> 到部分的顶部 \<Symbols> 。

       - 相对路径是由在清单的安装创作中定义的部署位置确定的。

3. 运行 **ManifestToCode** 工具以生成包装器，使现有代码具有可用于查询图像条的映像服务的名字对象。

   - 建议：为包装和命名空间提供非默认名称，以适合其使用情况。

4. 执行所有添加、安装程序创作/部署以及其他代码更改，以便使用映像服务和新文件。

   示例清单，包括内部和外部图像，以查看其外观：

```xml
<?xml version="1.0"?>
<ImageManifest
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">

  <Symbols>
    <!-- This needs to be the relative path from your manifest to the ImageCatalog's manifest
         where $(ManifestFolder) is the deployed location of this manifest. -->
    <Import Manifest="$(ManifestFolder)\<RelPath>\Microsoft.VisualStudio.ImageCatalog.imagemanifest" />

    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />
    <Guid Name="ImageGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />
    <Guid Name="ImageStripGuid" Value="{9c84a570-d9a7-4052-a340-188fb276f973}" />
    <ID Name="MyImage_0" Value="100" />
    <ID Name="MyImage_1" Value="101" />
    <ID Name="InternalList" Value="1001" />
    <ID Name="ExternalList" Value="1002" />
  </Symbols>

  <Images>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_0)">
      <Source Uri="$(Resources)/MyImage_0.png">
        <Size Value="16" />
      </Source>
    </Image>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_1)">
      <Source Uri="$(Resources)/MyImage_1.png">
        <Size Value="16" />
      </Source>
    </Image>
  </Images>

  <ImageLists>
    <ImageList Guid="$(ImageStripGuid)" ID="$(InternalList)">
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_0)" />
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_1)" />
    </ImageList>
    <ImageList Guid="$(ImageStripGuid)" ID="$(ExternalList)">
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusError)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusWarning)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusInformation)" External="true" />
    </ImageList>
  </ImageLists>

</ImageManifest>
```

 **我不需要支持 HIMAGELISTs**

1. 确定与图像条中的图像匹配的一组 **KnownMonikers** ，或在映像条中为图像创建自己的名字对象。

2. 更新在图像条的所需索引处获取图像所使用的任何映射，以改用名字对象。

3. 更新你的代码，以便使用映像服务通过已更新的映射来请求名字对象。  (这可能意味着要更新到托管代码的 **CrispImages** ，或者从映像服务请求 HBITMAPs 或 HICONs，并将其传递给本机代码。 ) 

## <a name="testing-your-images"></a>测试映像
 您可以使用 "图像库查看器" 工具来测试图像清单，以确保正确编写所有内容。 可以在[Visual Studio 2015 SDK](visual-studio-sdk.md)中找到该工具。 可在 [此处](./internals/vssdk-utilities.md?view=vs-2015&preserve-view=true)找到有关此工具和其他工具的文档。

## <a name="additional-resources"></a>其他资源

### <a name="samples"></a>示例
 已更新 GitHub 上的几个 Visual Studio 示例，以说明如何在各种 Visual Studio 扩展点中使用映像服务。

 检查 [http://github.com/Microsoft/VSSDK-Extensibility-Samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples) 最新的示例。

### <a name="tooling"></a>工具
 创建了一组用于映像服务的支持工具，以帮助创建/更新可与映像服务一起使用的 UI。 有关每个工具的详细信息，请查看工具随附的文档。 这些工具作为[2015 SDK Visual Studio一部分](visual-studio-sdk.md)。

 **ManifestFromResources**

 该工具Manifest from Resources PNG 或 XAML (映像资源的列表) 并生成一个映像清单文件，用于将这些映像与映像服务一起使用。

 **ManifestToCode**

 Manifest to Code工具采用映像清单文件，并生成一个包装文件，用于引用代码 (C++、C# 或 VB) *或 .vsct* 文件中清单值。

 **ImageLibraryViewer**

 图像库查看器工具可以加载图像清单，并允许用户以与确保正确创作Visual Studio相同的方式对其进行操作。 用户可以更改背景、大小、DPI 设置、高对比度和其他设置。 它还显示加载信息以查找清单中的错误，并显示清单中每个图像的源信息。

## <a name="faq"></a>常见问题解答

- 加载时，是否必须包含任何依赖项 \<Reference Include="Microsoft.VisualStudio.*.Interop.14.0.DesignTime" /> ？

  - 在所有互操作 DLL 上设置 EmbedInteropTypes="true"。

- 如何实现扩展部署映像清单？

  - 将 *.imagemanifest* 文件添加到项目。

  - 将"在 VSIX 中包括"设置为 True。

- 我正在更新 CPS Project System。 ImageName **和** **StockIconService 发生了什么** 情况？

  - 当 CPS 更新为使用名字对象时，已删除这些对象。 不再需要调用 **StockIconService，** 只需使用 CPS 实用工具中的 **ToProjectSystemType** () 扩展方法将所需的 **KnownMoniker** 传递给方法或属性。 可在下面找到从 **ImageName 到** **KnownMonikers 的** 映射：

    |**ImageName**|**KnownMoniker**|
    |-|-|
    |ImageName.OfflineWebApp|KnownImageIds.Web|
    |ImageName.WebReferencesFolder|KnownImageIds.Web|
    |ImageName.OpenReferenceFolder|KnownImageIds.FolderOpened|
    |ImageName.ReferenceFolder|KnownImageIds.Reference|
    |ImageName.Reference|KnownImageIds.Reference|
    |ImageName.SdlWebReference|KnownImageIds.WebReferenceFolder|
    |ImageName.DiscoWebReference|KnownImageIds.DynamicDiscoveryDocument|
    |ImageName.Folder|KnownImageIds.FolderClosed|
    |ImageName.OpenFolder|KnownImageIds.FolderOpened|
    |ImageName.ExcludedFolder|KnownImageIds.HiddenFolderClosed|
    |ImageName.OpenExcludedFolder|KnownImageIds.HiddenFolderOpened|
    |ImageName.ExcludedFile|KnownImageIds.HiddenFile|
    |ImageName.DependentFile|KnownImageIds.GenerateFile|
    |ImageName.MissingFile|KnownImageIds.DocumentWarning|
    |ImageName.WindowsForm|KnownImageIds.WindowsForm|
    |ImageName.WindowsUserControl|KnownImageIds.UserControl|
    |ImageName.WindowsComponent|KnownImageIds.ComponentFile|
    |ImageName.Xml架构|KnownImageIds.XML架构|
    |ImageName.Xml文件|KnownImageIds.XML文件|
    |ImageName.WebForm|KnownImageIds.Web|
    |ImageName.WebService|KnownImageIds.WebService|
    |ImageName.WebUserControl|KnownImageIds.WebUserControl|
    |ImageName.WebCustomUserControl|KnownImageIds.WebCustomControl|
    |ImageName.AspPage|KnownImageIds.ASPFile|
    |ImageName.GlobalApplicationClass|KnownImageIds.SettingsFile|
    |ImageName.WebConfig|KnownImageIds.ConfigurationFile|
    |ImageName.HtmlPage|KnownImageIds.HTMLFile|
    |ImageName.StyleSheet|KnownImageIds.StyleSheet|
    |ImageName.ScriptFile|KnownImageIds.JS脚本|
    |ImageName.TextFile|KnownImageIds.Document|
    |ImageName.SettingsFile|KnownImageIds。设置|
    |ImageName.Resources|KnownImageIds.DocumentGroup|
    |ImageName.Bitmap|KnownImageIds.Image|
    |ImageName.Icon|KnownImageIds.IconFile|
    |ImageName.Image|KnownImageIds.Image|
    |ImageName.ImageMap|KnownImageIds.ImageMapFile|
    |ImageName.XWorld|KnownImageIds.XWorldFile|
    |ImageName.Audio|KnownImageIds.Sound|
    |ImageName.Video|KnownImageIds.Media|
    |ImageName.Cab|KnownImageIds.CABProject|
    |ImageName|KnownImageIds. JARFile|
    |ImageName|KnownImageIds|
    |ImageName. PreviewFile|KnownImageIds|
    |ImageName. DanglingReference|KnownImageIds.ReferenceWarning|
    |ImageName. XsltFile|KnownImageIds. XSLTransform|
    |ImageName|KnownImageIds.CursorFile|
    |ImageName. AppDesignerFolder|KnownImageIds 属性|
    |ImageName|KnownImageIds|
    |ImageName|KnownImageIds|
    |ImageName|KnownImageIds.DatabaseGroup|
    |ImageName .Pfx|KnownImageIds|
    |ImageName|KnownImageIds|
    |ImageName. VisualBasicProject|KnownImageIds.VBProjectNode|
    |ImageName. CSharpProject|KnownImageIds.CSProjectNode|
    |ImageName|KnownImageIds 空白|
    |ImageName. MissingFolder|KnownImageIds.FolderOffline|
    |ImageName. SharedImportReference|KnownImageIds.SharedProject|
    |ImageName. SharedProjectCs|KnownImageIds.CSSharedProject|
    |ImageName. SharedProjectVc|KnownImageIds.CPPSharedProject|
    |ImageName. SharedProjectJs|KnownImageIds.JSSharedProject|
    |ImageName. CSharpCodeFile|KnownImageIds.CSFileNode|
    |ImageName. VisualBasicCodeFile|KnownImageIds.VBFileNode|

  - 我正在更新完成列表提供程序。 哪些 **KnownMonikers** 与旧的 **StandardGlyphGroup** 和 **StandardGlyph** 值匹配？

    |名称|名称|名称|
    |-|-|-|
    |GlyphGroupClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupConstant|GlyphItemPublic|ConstantPublic|
    |GlyphGroupConstant|GlyphItemInternal|ConstantInternal|
    |GlyphGroupConstant|GlyphItemFriend|ConstantInternal|
    |GlyphGroupConstant|GlyphItemProtected|ConstantProtected|
    |GlyphGroupConstant|GlyphItemPrivate|ConstantPrivate|
    |GlyphGroupConstant|GlyphItemShortcut|ConstantShortcut|
    |GlyphGroupDelegate|GlyphItemPublic|DelegatePublic|
    |GlyphGroupDelegate|GlyphItemInternal|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemFriend|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemProtected|DelegateProtected|
    |GlyphGroupDelegate|GlyphItemPrivate|DelegatePrivate|
    |GlyphGroupDelegate|GlyphItemShortcut|DelegateShortcut|
    |GlyphGroupEnum|GlyphItemPublic|EnumerationPublic|
    |GlyphGroupEnum|GlyphItemInternal|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemFriend|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemProtected|EnumerationProtected|
    |GlyphGroupEnum|GlyphItemPrivate|EnumerationPrivate|
    |GlyphGroupEnum|GlyphItemShortcut|EnumerationShortcut|
    |GlyphGroupEnumMember|GlyphItemPublic|EnumerationItemPublic|
    |GlyphGroupEnumMember|GlyphItemInternal|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemFriend|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemProtected|EnumerationItemProtected|
    |GlyphGroupEnumMember|GlyphItemPrivate|EnumerationItemPrivate|
    |GlyphGroupEnumMember|GlyphItemShortcut|EnumerationItemShortcut|
    |GlyphGroupEvent|GlyphItemPublic|EventPublic|
    |GlyphGroupEvent|GlyphItemInternal|EventInternal|
    |GlyphGroupEvent|GlyphItemFriend|EventInternal|
    |GlyphGroupEvent|GlyphItemProtected|EventProtected|
    |GlyphGroupEvent|GlyphItemPrivate|EventPrivate|
    |GlyphGroupEvent|GlyphItemShortcut|EventShortcut|
    |GlyphGroupException|GlyphItemPublic|ExceptionPublic|
    |GlyphGroupException|GlyphItemInternal|ExceptionInternal|
    |GlyphGroupException|GlyphItemFriend|ExceptionInternal|
    |GlyphGroupException|GlyphItemProtected|ExceptionProtected|
    |GlyphGroupException|GlyphItemPrivate|ExceptionPrivate|
    |GlyphGroupException|GlyphItemShortcut|ExceptionShortcut|
    |GlyphGroupField|GlyphItemPublic|FieldPublic|
    |GlyphGroupField|GlyphItemInternal|FieldInternal|
    |GlyphGroupField|GlyphItemFriend|FieldInternal|
    |GlyphGroupField|GlyphItemProtected|FieldProtected|
    |GlyphGroupField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupMacro|GlyphItemPublic|MacroPublic|
    |GlyphGroupMacro|GlyphItemInternal|MacroInternal|
    |GlyphGroupMacro|GlyphItemFriend|MacroInternal|
    |GlyphGroupMacro|GlyphItemProtected|MacroProtected|
    |GlyphGroupMacro|GlyphItemPrivate|MacroPrivate|
    |GlyphGroupMacro|GlyphItemShortcut|MacroShortcut|
    |GlyphGroupMap|GlyphItemPublic|MapPublic|
    |GlyphGroupMap|GlyphItemInternal|MapInternal|
    |GlyphGroupMap|GlyphItemFriend|MapInternal|
    |GlyphGroupMap|GlyphItemProtected|MapProtected|
    |GlyphGroupMap|GlyphItemPrivate|MapPrivate|
    |GlyphGroupMap|GlyphItemShortcut|MapShortcut|
    |GlyphGroupMapItem|GlyphItemPublic|MapItemPublic|
    |GlyphGroupMapItem|GlyphItemInternal|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemFriend|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemProtected|MapItemProtected|
    |GlyphGroupMapItem|GlyphItemPrivate|MapItemPrivate|
    |GlyphGroupMapItem|GlyphItemShortcut|MapItemShortcut|
    |GlyphGroupMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupOverload|GlyphItemPublic|MethodPublic|
    |GlyphGroupOverload|GlyphItemInternal|MethodInternal|
    |GlyphGroupOverload|GlyphItemFriend|MethodInternal|
    |GlyphGroupOverload|GlyphItemProtected|MethodProtected|
    |GlyphGroupOverload|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupOverload|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupModule|GlyphItemPublic|ModulePublic|
    |GlyphGroupModule|GlyphItemInternal|ModuleInternal|
    |GlyphGroupModule|GlyphItemFriend|ModuleInternal|
    |GlyphGroupModule|GlyphItemProtected|ModuleProtected|
    |GlyphGroupModule|GlyphItemPrivate|ModulePrivate|
    |GlyphGroupModule|GlyphItemShortcut|ModuleShortcut|
    |GlyphGroupNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupOperator|GlyphItemPublic|OperatorPublic|
    |GlyphGroupOperator|GlyphItemInternal|OperatorInternal|
    |GlyphGroupOperator|GlyphItemFriend|OperatorInternal|
    |GlyphGroupOperator|GlyphItemProtected|OperatorProtected|
    |GlyphGroupOperator|GlyphItemPrivate|OperatorPrivate|
    |GlyphGroupOperator|GlyphItemShortcut|OperatorShortcut|
    |GlyphGroupProperty|GlyphItemPublic|PropertyPublic|
    |GlyphGroupProperty|GlyphItemInternal|PropertyInternal|
    |GlyphGroupProperty|GlyphItemFriend|PropertyInternal|
    |GlyphGroupProperty|GlyphItemProtected|PropertyProtected|
    |GlyphGroupProperty|GlyphItemPrivate|PropertyPrivate|
    |GlyphGroupProperty|GlyphItemShortcut|PropertyShortcut|
    |GlyphGroupStruct|GlyphItemPublic|StructurePublic|
    |GlyphGroupStruct|GlyphItemInternal|StructureInternal|
    |GlyphGroupStruct|GlyphItemFriend|StructureInternal|
    |GlyphGroupStruct|GlyphItemProtected|StructureProtected|
    |GlyphGroupStruct|GlyphItemPrivate|StructurePrivate|
    |GlyphGroupStruct|GlyphItemShortcut|StructureShortcut|
    |GlyphGroupTemplate|GlyphItemPublic|TemplatePublic|
    |GlyphGroupTemplate|GlyphItemInternal|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemFriend|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemProtected|TemplateProtected|
    |GlyphGroupTemplate|GlyphItemPrivate|TemplatePrivate|
    |GlyphGroupTemplate|GlyphItemShortcut|TemplateShortcut|
    |GlyphGroupTypedef|GlyphItemPublic|TypeDefinitionPublic|
    |GlyphGroupTypedef|GlyphItemInternal|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemFriend|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemProtected|TypeDefinitionProtected|
    |GlyphGroupTypedef|GlyphItemPrivate|TypeDefinitionPrivate|
    |GlyphGroupTypedef|GlyphItemShortcut|TypeDefinitionShortcut|
    |GlyphGroupType|GlyphItemPublic|TypePublic|
    |GlyphGroupType|GlyphItemInternal|TypeInternal|
    |GlyphGroupType|GlyphItemFriend|TypeInternal|
    |GlyphGroupType|GlyphItemProtected|TypeProtected|
    |GlyphGroupType|GlyphItemPrivate|TypePrivate|
    |GlyphGroupType|GlyphItemShortcut|TypeShortcut|
    |GlyphGroupUnion|GlyphItemPublic|UnionPublic|
    |GlyphGroupUnion|GlyphItemInternal|UnionInternal|
    |GlyphGroupUnion|GlyphItemFriend|UnionInternal|
    |GlyphGroupUnion|GlyphItemProtected|UnionProtected|
    |GlyphGroupUnion|GlyphItemPrivate|UnionPrivate|
    |GlyphGroupUnion|GlyphItemShortcut|UnionShortcut|
    |GlyphGroupVariable|GlyphItemPublic|FieldPublic|
    |GlyphGroupVariable|GlyphItemInternal|FieldInternal|
    |GlyphGroupVariable|GlyphItemFriend|FieldInternal|
    |GlyphGroupVariable|GlyphItemProtected|FieldProtected|
    |GlyphGroupVariable|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupVariable|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupValueType|GlyphItemPublic|ValueTypePublic|
    |GlyphGroupValueType|GlyphItemInternal|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemFriend|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemProtected|ValueTypeProtected|
    |GlyphGroupValueType|GlyphItemPrivate|ValueTypePrivate|
    |GlyphGroupValueType|GlyphItemShortcut|ValueTypeShortcut|
    |GlyphGroupIntrinsic|GlyphItemPublic|ObjectPublic|
    |GlyphGroupIntrinsic|GlyphItemInternal|ObjectInternal|
    |GlyphGroupIntrinsic|GlyphItemFriend|ObjectInternal|
    |GlyphGroupIntrinsic|GlyphItemProtected|ObjectProtected|
    |GlyphGroupIntrinsic|GlyphItemPrivate|ObjectPrivate|
    |GlyphGroupIntrinsic|GlyphItemShortcut|ObjectShortcut|
    |GlyphGroupJSharpMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupJSharpMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupJSharpMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupJSharpMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupJSharpField|GlyphItemPublic|FieldPublic|
    |GlyphGroupJSharpField|GlyphItemInternal|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemFriend|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemProtected|FieldProtected|
    |GlyphGroupJSharpField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupJSharpField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupJSharpClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupJSharpClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupJSharpClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupJSharpClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupJSharpNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupJSharpNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupJSharpNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupJSharpNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupJSharpInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupJSharpInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupJSharpInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupJSharpInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupError||StatusError|
    |GlyphBscFile||ClassFile|
    |GlyphAssembly||参考|
    |GlyphLibrary||库|
    |GlyphVBProject||VBProjectNode|
    |GlyphCoolProject||CSProjectNode|
    |GlyphCppProject||CPPProjectNode|
    |GlyphDialogId||对话框|
    |GlyphOpenFolder||FolderOpened|
    |GlyphClosedFolder||FolderClosed|
    |GlyphArrow||GoToNext|
    |GlyphCSharpFile||CSFileNode|
    |GlyphCSharpExpansion||片段|
    |GlyphKeyword||IntellisenseKeyword|
    |GlyphInformation||StatusInformation|
    |GlyphReference||ClassMethodReference|
    |GlyphRecursion||递归|
    |GlyphXmlItem||标记|
    |GlyphJSharpProject||DocumentCollection|
    |GlyphJSharpDocument||文档|
    |GlyphForwardType||GoToNext|
    |GlyphCallersGraph||CallTo|
    |GlyphCallGraph||CallFrom|
    |GlyphWarning||StatusWarning|
    |GlyphMaybeReference||QuestionMark|
    |GlyphMaybeCaller||CallTo|
    |GlyphMaybeCall||CallFrom|
    |GlyphExtensionMethod||ExtensionMethod|
    |GlyphExtensionMethodInternal||ExtensionMethod|
    |GlyphExtensionMethodFriend||ExtensionMethod|
    |GlyphExtensionMethodProtected||ExtensionMethod|
    |GlyphExtensionMethodPrivate||ExtensionMethod|
    |GlyphExtensionMethodShortcut||ExtensionMethod|
    |GlyphXmlAttribute||XmlAttribute|
    |GlyphXmlChild||XmlElement|
    |GlyphXmlDescendant||XmlDescendant|
    |GlyphXmlNamespace||XmlNamespace|
    |GlyphXmlAttributeQuestion||XmlAttributeLowConfidence|
    |GlyphXmlAttributeCheck||XmlAttributeHighConfidence|
    |GlyphXmlChildQuestion||XmlElementLowConfidence|
    |GlyphXmlChildCheck||XmlElementHighConfidence|
    |GlyphXmlDescendantQuestion||XmlDescendantLowConfidence|
    |GlyphXmlDescendantCheck||XmlDescendantHighConfidence|
    |GlyphCompletionWarning||IntellisenseWarning|
