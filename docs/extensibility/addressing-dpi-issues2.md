---
title: 解决 DPI 问题2 |Microsoft Docs
description: 了解高分辨率屏幕编程所涉及的问题，例如纵向扩展内容、布局问题以及使用 DPI 缩放 API。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3ca4544b153d5b365d3200a79a519cf6271d29bc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122133401"
---
# <a name="address-dpi-issues"></a>解决 DPI 问题
越来越多的设备通过"高分辨率"屏幕交付。 这些屏幕通常具有每英寸超过 200 像素的 ppi (像素) 。 在这些计算机上使用应用程序需要扩展内容，以满足在设备的正常查看距离查看内容的需求。 截至 2014 年，高密度显示器的主要目标是移动计算设备 (平板电脑、) 。

Windows 8.1及更高版本包含多个功能，使这些计算机能够同时连接到高密度和标准密度显示器的显示器和环境。

- Windows自 Windows XP 以来，可以使用"使文本和其他项更大或更小"设置将内容 (设备) 。

- Windows 8.1和更高版本将自动缩放内容，使大多数应用程序在不同像素密度的显示之间移动时保持一致。 当主显示器是高密度 (200% 缩放) 且辅助显示器是标准密度 (100%) 时，Windows 将自动将辅助显示器上的应用程序窗口内容缩减 (为 1 像素，每 4 像素显示一次应用程序) 。

- Windows将默认为像素密度和显示器 7 (Windows观看距离的合适缩放，OEM 可配置) 。

- Windows S14 Windows 8.1，在超过 280 ppi 的新设备上， (自动将内容缩放) 。

  Windows可以处理纵向扩展 UI，以利用增加的像素计数。 应用程序通过声明自身"系统 DPI 感知"来选择加入此系统。 不这样做的应用程序由系统进行扩展。 这可能会导致整个应用程序均匀拉伸像素的"模糊"用户体验。 例如：

  ![DPI 问题 模糊](../extensibility/media/dpi-issues-fuzzy.png "DPI 问题 模糊")

  Visual Studio DPI 缩放感知，因此不会"虚拟化"。

  Windows (Visual Studio) 多种 UI 技术，这些技术处理系统设置的缩放因素的方法各不相同。 例如：

- WPF 以与设备无关的方式度量控件， (单位，而不是像素) 。 WPF UI 会自动针对当前 DPI 进行扩展。

- 无论 UI 框架如何，所有文本大小都以点表示，因此系统将视为与 DPI 无关。 在绘制到显示设备时，Win32、WinForms 和 WPF 中的文本已正确扩展。

- Win32/WinForms 对话框和窗口具有启用布局（例如，通过网格、流和表布局面板） (调整文本大小的方式) 。 这样可以避免在增加字号时不缩放的硬编码像素位置。

- 系统提供的图标或基于系统指标的资源 (例如，SM_CXICON和SM_CXSMICON) 已扩展。

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>旧版 Win32 (GDI、GDI+) 和基于 WinForms 的 UI
虽然 WPF 已具有高 DPI 感知能力，但许多基于 Win32/GDI 的代码最初并未在编写时考虑 DPI 感知。 Windows提供了 DPI 缩放 API。 Win32 问题的修复应在整个产品内一致地使用这些解决方案。 Visual Studio提供了帮助程序类库，以避免重复功能并确保产品之间的一致性。

## <a name="high-resolution-images"></a>高分辨率图像
本部分主要面向扩展 Visual Studio 2013。 对于 Visual Studio 2015，请使用内置于 Visual Studio。 你可能还发现需要支持/面向许多版本的 Visual Studio因此在 2015 年使用映像服务不是一个选项，因为它在以前的版本中不存在。 本部分也供你使用。

## <a name="scaling-up-images-that-are-too-small"></a>纵向扩展太小的图像
对于太小的图像，可以使用一些常用方法在 GDI 和 WPF 上进行扩展和呈现。 托管 DPI 帮助程序类可供内部和外部集成Visual Studio处理缩放图标、位图、图像带和图像列表。 基于 Win32 的本机 C/C++ 帮助程序可用于缩放 HICON、HBITMAP、HIMAGELIST 和 VsUI：：GdiplusImage。 缩放位图通常只需要在包含对帮助程序库的引用后进行单行更改。 例如：

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

缩放映像列表取决于映像列表是在加载时完成还是运行时追加。 如果在加载时完成，则 `LogicalToDeviceUnits()` 使用图像列表调用 ，就像使用位图一样。 当代码需要在编写图像列表之前加载单个位图时，请确保缩放图像列表的图像大小：

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

在本机代码中，可以在创建映像列表时缩放维度，如下所示：

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

库中的函数允许指定调整大小算法。 缩放要放入图像列表的图像时，请确保指定用于透明度的背景色，或使用 NearestNeighbor 缩放 (这会造成 125% 和 150% ) 。

请参阅 <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> MSDN 上的文档。

下表显示了如何按相应的 DPI 缩放因子缩放图像的示例。 橙色图像 Visual Studio 2013 (表示从 100%-200% DPI 缩放到 100%-200%) ：

![DPI 问题 缩放](../extensibility/media/dpi-issues-scaling.png "DPI 问题 缩放")

## <a name="layout-issues"></a>布局问题
主要可以通过使 UI 中的点缩放并彼此相对，而不是使用绝对位置来避免常见的布局 (具体说来，以像素单位表示) 。 例如：

- 布局/文本位置需要进行调整，以考虑到已扩展的图像。

- 网格中的列需要调整扩展文本的宽度。

- 还需要增加硬编码的大小或元素之间的空间。 仅基于文本维度的大小通常很正常，因为字体会自动增加。

  类中提供了帮助程序 <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> 函数，以允许在 X 轴和 Y 轴上缩放：

- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (函数允许在 X/Y 轴上缩放) 

- int space = DpiHelper.LogicalToDeviceUnitsX (10) ;

- int height = VsUI：:D piHelper：：LogicalToDeviceUnitsY (5) ;

  存在 LogicalToDeviceUnits 重载，允许缩放对象，如矩形、点和大小。

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>使用 DPIHelper 库/类缩放图像和布局
Visual Studio DPI 帮助程序库以本机和托管形式提供，并且可在 Visual Studio shell 外部供其他应用程序使用。

若要使用该库，请转到[VSSDK Visual Studio示例，](https://github.com/Microsoft/VSSDK-Extensibility-Samples)并克隆该High-DPI_Images_Icons示例。

在源文件中，包括 *VsUIDpiHelper.h* 并调用 类的静态 `VsUI::DpiHelper` 函数：

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> 请勿在模块级或类级静态变量中使用帮助程序函数。 该库还使用静态进行线程同步，你可能会遇到顺序初始化问题。 将这些静态变量转换为非静态成员变量，或将它们包装到函数 (以便它们在首次访问时构造) 。

若要从将在托管环境中运行的托管代码中访问 DPI 帮助Visual Studio函数：

- 使用项目必须引用最新版本的 Shell MPF。 例如：

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- 确保项目具有对 **System.Windows 的引用。窗体** **、PresentationCore** 和 **PresentationUI。**

- 在代码中，使用 **Microsoft.VisualStudio.PlatformUI** 命名空间并调用 DpiHelper 类的静态函数。 对于支持的 (点、大小、矩形等) ，提供了返回新缩放对象的扩展函数。 例如：

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>处理可缩放 UI 中的 WPF 图像模糊性
在 WPF 中，WPF 使用高质量双维算法 (默认) 自动调整当前 DPI 缩放级别的位图大小，该算法适用于图片或大型屏幕截图，但不适合菜单项图标，因为它引入了感知模糊性。

建议：

- 对于徽标图像和横幅图稿，可能会 <xref:System.Windows.Media.BitmapScalingMode> 使用默认的调整大小模式。

- 对于菜单项和图标图像，当 不会导致其他扭曲项目消除模糊化时， (<xref:System.Windows.Media.BitmapScalingMode> 200% 和 300%) 。

- 对于不为 100% (倍数（例如，250% 或 350%) ）的大型缩放级别，缩放具有二元效果的图标图像会导致模糊、模糊的 UI。 通过首先将具有 NearestNeighbor 的图像缩放为 100% (的最大倍数（例如，200% 或 300%) ）以及从该位置缩放双倍数，可以获得更好的结果。 有关详细信息，请参阅特殊情况：为较大的 DPI 级别预缩放 WPF 图像。

  Microsoft.VisualStudio.PlatformUI 命名空间中的 DpiHelper 类提供可用于 <xref:System.Windows.Media.BitmapScalingMode> 绑定的成员。 它将允许 Visual Studio shell 统一控制产品中的位图缩放模式，具体取决于 DPI 缩放因子。

  若要在 XAML 中使用它，请添加：

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

命令行Visual Studio shell 已在顶级窗口和对话框中设置此属性。 在 Visual Studio 中运行的基于 WPF 的 UI 已继承它。 如果设置未传播到特定 UI 片段，可以在 XAML/WPF UI 的根元素上设置此设置。 发生这种情况的位置包括弹出窗口、具有 Win32 父元素的元素和进程外设计器窗口（如 Blend）。

某些 UI 可以独立于系统设置的 DPI 缩放级别进行缩放，例如基于 Visual Studio 文本编辑器和基于 WPF 的设计器 (WPF Desktop 和 Windows Store) 。 在这些情况下，不应使用 DpiHelper.BitmapScalingMode。 为了在编辑器中解决此问题，IDE 团队创建了一个标题为 RenderOptions.BitmapScalingMode 的自定义属性。 根据系统和 UI 的组合缩放级别，将属性值设置为 HighQuality 或 NearestNeighbor。

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>特例： prescaling 适用于大型 DPI 级别的 WPF 映像
对于不是 100% (的倍数的非常大的缩放级别（例如250%、350% 等) ），通过双立方缩放插图图像会导致模糊的、冲蚀的 UI。 这些图像与明锐文本的印象几乎与一种视觉效果一样。 图像看起来更接近于与文本相关的眼睛和焦点。 通过首先将具有 NearestNeighbor 的图像缩放为 100% (的最大倍数，例如200% 或 300% ) 并使用三倍调整到剩余部分 (额外的 50% ) ，可以提高此放大大小的缩放结果。

下面是结果差异的示例，其中，第一个图像使用改进后的双缩放算法 100%->200%->250%，第二个图像使用三倍双精度 100%->250%。

![DPI 问题双缩放示例](../extensibility/media/dpi-issues-double-scaling-example.png "DPI 问题双缩放示例")

为了使 UI 能够使用这种双缩放，需要修改用于显示每个图像元素的 XAML 标记。 下面的示例演示如何在使用 DpiHelper 库和 Shell 的 Visual Studio 中使用 WPF 进行双重缩放。

步骤1：使用 NearestNeighbor 将图像 Prescale 为200%、300% 等。

使用应用于绑定的转换器或使用 XAML 标记扩展 Prescale 图像。 例如：

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

如果还需要对映像进行主题 (大多数情况下（如果不是全部）都应该) ，则标记可以使用第一种转换器，该转换器首先执行图像的主题，然后进行预缩放。 标记可以使用 <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> 或 <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter> ，具体取决于所需的转换输出。

```xaml
<vsui:DpiPrescaleThemedImageSourceConverter x:Key="DpiPrescaleThemedImageSourceConverter" />

<Image Width="16" Height="16">
  <Image.Source>
    <MultiBinding Converter="{StaticResource DpiPrescaleThemedImageSourceConverter}">
      <Binding Path="Icon" />
      <Binding Path="(vsui:ImageThemingUtilities.ImageBackgroundColor)"
               RelativeSource="{RelativeSource Self}" />
      <Binding Source="{x:Static vsui:Boxes.BooleanTrue}" />
    </MultiBinding>
  </Image.Source>
</Image>
```

步骤2：确保最终大小对于当前 DPI 是正确的。

因为 WPF 将使用 UIElement 上设置的 System.windows.media.bitmapscalingmode> 属性缩放当前 DPI 的 UI，所以，使用 prescaled 图像作为其源的图像控件的外观将会比它的大小大两倍。 下面是用于应对这种效果的几种方法：

- 如果您知道原始图像在100% 的维度，则可以指定图像控件的精确大小。 在应用缩放之前，这些大小将反映 UI 的大小。

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- 如果原始映像的大小未知，则可以使用 System.windows.frameworkelement.layouttransform 来缩减最终图像对象。 例如：

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>为 WebOC 启用 HDPI 支持
默认情况下，WebOC 控件 (如 WPF 中的 WebBrowser 控件或 IWebBrowser2 接口) 不启用 HDPI 检测和支持。 结果将是在高分辨率显示器上显示内容太小的嵌入控件。 下面介绍如何在特定的 web WebOC 实例中启用高 DPI 支持。

实现 IDocHostUIHandler 接口 (参阅 [IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85))上的 MSDN 文章：

```idl
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("BD3F23C0-D43E-11CF-893B-00AA00BDCE1A")]
public interface IDocHostUIHandler
{
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowContextMenu(
        [In, MarshalAs(UnmanagedType.U4)] int dwID,
        [In] POINT pt,
        [In, MarshalAs(UnmanagedType.Interface)] object pcmdtReserved,
        [In, MarshalAs(UnmanagedType.IDispatch)] object pdispReserved);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetHostInfo([In, Out] DOCHOSTUIINFO info);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowUI(
        [In, MarshalAs(UnmanagedType.I4)] int dwID,
        [In, MarshalAs(UnmanagedType.Interface)] object activeObject,
        [In, MarshalAs(UnmanagedType.Interface)] object commandTarget,
        [In, MarshalAs(UnmanagedType.Interface)] object frame,
        [In, MarshalAs(UnmanagedType.Interface)] object doc);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int HideUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int UpdateUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int EnableModeless([In, MarshalAs(UnmanagedType.Bool)] bool fEnable);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnDocWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnFrameWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ResizeBorder(
        [In] COMRECT rect,
        [In, MarshalAs(UnmanagedType.Interface)] object doc,
        bool fFrameWindow);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateAccelerator(
        [In] ref MSG msg,
        [In] ref Guid group,
        [In, MarshalAs(UnmanagedType.I4)] int nCmdID);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetOptionKeyPath(
        [Out, MarshalAs(UnmanagedType.LPArray)] string[] pbstrKey,
        [In, MarshalAs(UnmanagedType.U4)] int dw);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetDropTarget(
        [In, MarshalAs(UnmanagedType.Interface)] IOleDropTarget pDropTarget,
        [MarshalAs(UnmanagedType.Interface)] out IOleDropTarget ppDropTarget);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateUrl(
        [In, MarshalAs(UnmanagedType.U4)] int dwTranslate,
        [In, MarshalAs(UnmanagedType.LPWStr)] string strURLIn,
        [MarshalAs(UnmanagedType.LPWStr)] out string pstrURLOut);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int FilterDataObject(
        IDataObject pDO,
        out IDataObject ppDORet);
    }
```

或者，实现 ICustomDoc 接口 (参阅 [ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85))上的 MSDN 文章：

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

将实现 IDocHostUIHandler 的类与 WebOC 的文档相关联。 如果在上面实现了 ICustomDoc 接口，则 WebOC 的文档属性有效后，会立即将其转换为 ICustomDoc，并调用 SetUIHandler 方法，同时传递实现 IDocHostUIHandler 的类。

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

如果未实现 ICustomDoc 接口，则只要 WebOC 的文档属性有效，就需要将其强制转换为 IOleObject，并调用 `SetClientSite` 方法，并传入实现 IDocHostUIHandler 的类。 将 DOCHOSTUIINFO 上的 DOCHOSTUIFLAG_DPI_AWARE 标志设置为传递给 `GetHostInfo` 方法调用：

```csharp
public int GetHostInfo(DOCHOSTUIINFO info)
{
    // This is what the default site provides.
    info.dwFlags = (DOCHOSTUIFLAG)0x5a74012;
    // Add the DPI flag to the defaults
    info.dwFlags |=.DOCHOSTUIFLAG.DOCHOSTUIFLAG_DPI_AWARE;
    return S_OK;
}
```

这应该是使 WebOC 控件支持 HPDI 所需的全部工作。

## <a name="tips"></a>提示

1. 如果 WebOC 控件上的文档属性更改，则可能需要将文档与 IDocHostUIHandler 类重新关联。

2. 如果上述操作不起作用，则会出现一个已知问题，WebOC 不会选取 DPI 标志。 解决这种情况的最可靠方法是切换 WebOC 的光纤缩放，这意味着，两次调用具有两个不同的值来表示缩放百分比。 此外，如果需要解决此问题，则可能需要对每个导航调用执行此方法。

    ```csharp
    // browser2 is a SHDocVw.IWebBrowser2 in this case
    // EX: Call the Exec twice with DPI%-1 and then DPI% as the zoomPercent values
    IOleCommandTarget cmdTarget = browser2.Document as IOleCommandTarget;
    if (cmdTarget != null)
    {
        object commandInput = zoomPercent;
        cmdTarget.Exec(IntPtr.Zero,
                       OLECMDID_OPTICAL_ZOOM,
                       OLECMDEXECOPT_DONTPROMPTUSER,
                       ref commandInput,
                       ref commandOutput);
    }
    ```
