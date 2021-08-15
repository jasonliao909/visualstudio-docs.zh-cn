---
title: 样式的颜色和Visual Studio |Microsoft Docs
description: 了解Visual Studio用户体验如何使用颜色作为通信工具，而不是出于纯美观的原因。
ms.custom: SEO-VS-2020
ms.date: 07/31/2017
ms.topic: reference
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ec263080835d6e83141fb7f24b40342cfd87ea31e686d4954f60a432b8ca9884
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375191"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio 的颜色和样式

## <a name="use-color-in-visual-studio"></a>使用颜色Visual Studio

在Visual Studio中，颜色主要用作通信工具，而不只是修饰。 尽可能少使用颜色，并保留颜色以用于需要：

- 传达含义或 (关系，例如平台或语言修饰符) 

- 例如 (，指示状态更改) 

- 提高可读性并提供用于导航 UI 的地标

- 提高可读性

有几个选项用于将颜色分配给 Visual Studio 中的 UI 元素。 有时，可能很难确定应该使用哪个选项，或者如何正确使用它。 本主题将帮助你：

- 了解用于定义颜色的不同服务和系统Visual Studio。

- 为给定元素选择正确的选项。

- 正确使用所选选项。

> [!NOTE]
> 切勿将十六进制、RGB 或系统颜色硬编码到 UI 元素。 使用服务可以灵活地优化色调。 此外，如果没有该服务，将无法利用 VSColor 服务 的主题 [切换功能](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>用于向接口元素Visual Studio颜色的方法

选择最适合 UI 元素的方法。

| Your UI | 方法 | 分别是哪两个参数？ |
| --- | --- | --- |
| 已嵌入或独立的对话框。 | **系统颜色** | 允许操作系统定义 UI 元素的颜色和外观的系统名称，如常见的对话框控件。 |
| 自定义 UI 希望与整体 VS 环境保持一致，并且具有与共享令牌的类别和语义含义匹配的 UI 元素。 | **常见共享颜色** | 特定 UI 元素的现有预定义颜色标记名称 |
| 你有一个特征或一组特征，没有类似元素的共享颜色。 | **自定义颜色** | 特定于区域且不应与其他 UI 共享的颜色标记名称 |
| 你想要允许最终用户自定义 UI 或内容，例如 (编辑器或专用设计器窗口) 。 | **最终用户自定义**<br /><br />**(工具 &gt; 选项"对话框)** | 设置"工具选项"对话框的"字体和颜色"页中定义 **， &gt;** 或特定于一个 UI 功能的特定页面。 |

### <a name="visual-studio-themes"></a>Visual Studio主题

Visual Studio三种不同的颜色主题：浅色、深色和蓝色。 它还检测高对比度模式，这是专为辅助功能设计的系统范围颜色主题。

第一次使用 Visual Studio 时，系统会提示用户选择主题，稍后可以切换到"工具""选项环境""常规"，然后从"颜色主题"下拉菜单中选择新主题。 **&gt; &gt; &gt;**

用户还可使用控制面板将整个系统切换为多个主题高对比度之一。 如果用户选择 高对比度 主题，Visual Studio 颜色主题选择器将不再影响 Visual Studio 中的颜色，尽管当用户退出 高对比度 模式时，将保存任何主题更改。 有关模式高对比度，请参阅 [选择高对比度颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)。

### <a name="the-vscolor-service"></a>VSColor 服务

Visual Studio环境颜色服务（称为 VSColor 服务），通过该服务，你可以将 UI 元素的颜色值绑定到包含每个主题的颜色值的命名Visual Studio项。 这可确保颜色自动更改以反映当前用户选择的主题或系统高对比度模式。 使用服务意味着所有与主题相关的颜色更改的实现在一处进行处理，如果使用的是服务中的常见共享颜色，则 UI 将自动反映未来版本的 Visual Studio。

### <a name="implementation"></a>实现

该Visual Studio包括多个包定义文件，其中包含令牌名称列表以及每个主题各自的颜色值。 颜色服务读取这些包定义文件中定义的 VSColors。 这些颜色在 XAML 标记或代码中引用，然后通过 方法或 `IVsUIShell5.GetThemedColor` DynamicResource 映射加载。

### <a name="system-colors"></a>系统颜色

默认情况下，公共控件引用系统颜色。 如果希望 UI 使用系统颜色，例如创建嵌入或独立对话框时，无需执行任何操作。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor 服务中的常见共享颜色

接口元素应反映整个Visual Studio环境。 通过使用适用于正在设计的 UI 组件的常用共享颜色，可以确保接口与其他 Visual Studio 接口一致，并且颜色在添加或更新主题时自动更新。

在使用常用共享颜色之前，请确保了解如何正确使用它们。 错误地使用常见共享颜色可能会导致用户体验不一致、令人困惑或令人困惑。

### <a name="user-customizable-colors"></a>用户可自定义的颜色

请参阅： [向最终用户公开颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

有时，需要允许最终用户自定义 UI，就像创建代码编辑器或设计图面时一样。 可在"工具选项"对话框的"字体和颜色"部分找到可自定义的 UI 组件，用户可以选择更改前景色和/或背景色。 **&gt;**

![" &gt; 工具选项"对话框](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />" &gt; 工具选项"对话框

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a> VSColor 服务

Visual Studio环境颜色服务，也称为 VSColor 服务或 shell 颜色服务。 此服务允许你将 UI 元素的颜色值绑定到包含每个主题的颜色的名称/值颜色集。 VSColor 服务必须用于所有 UI 元素，以便颜色自动更改以反映当前用户选择的主题，因此绑定到环境颜色服务的 UI 将在未来版本的 Visual Studio 中与新主题集成。

### <a name="how-the-service-works"></a>服务的工作原理

环境颜色服务读取在 UI 组件的 .pkgdef 中定义的 VSColors。 然后，这些 VSColors 在 XAML 标记或代码中引用，并通过 或 `IVsUIShell5.GetThemedColor` 映射 `DynamicResource` 加载。

![环境颜色服务体系结构](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />环境颜色服务体系结构

### <a name="accessing-the-service"></a>访问服务

根据你使用的颜色令牌类型以及你拥有的代码类型，有几种不同的方法来访问 VSColor 服务。

#### <a name="predefined-environment-colors"></a>预定义的环境颜色

##### <a name="from-native-code"></a>从本机代码

shell 提供一个服务，用于 `COLORREF` 访问颜色的 。 服务/接口为：

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

在 VSShell80.idl 文件中，枚举 `__VSSYSCOLOREX` 具有 shell 颜色常量。 若要使用它，请从 MSDN 中记录的值之一或系统 API 接受的常规索引Windows作为索引 `enum __VSSYSCOLOREX` `GetSysColor` 值。 执行此操作会返回应在第二个参数中使用的颜色的 RGB 值。

如果存储具有新颜色的笔或画笔，则必须 (shell Visual Studio，) `AdviseBroadcastMessages` 侦听 和 `WM_SYSCOLORCHANGE` `WM_THEMECHANGED` 消息。

若要在本机代码中访问颜色服务，需要执行类似于下面的调用：

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> `COLORREF`返回的值仅 `GetVSSysColorEx()` 包含主题颜色的 R、G、B 组件。 如果主题项使用透明度，则返回之前将丢弃 alpha 通道值。 因此，如果需要在透明度通道重要的位置使用感兴趣的环境颜色，则应该使用 而不是 ，如本主题稍后 `IVsUIShell5.GetThemedColor` `IVsUIShell2::GetVSSysColorEx` 所述。

##### <a name="from-managed-code"></a>从托管代码

通过本机代码访问 VSColor 服务非常简单。 但是，如果正在处理托管代码，则确定如何使用服务可能比较棘手。 请记住这一点，下面是演示此过程的 C# 代码片段：

```csharp
private void VSColorPaint(object sender, System.Windows.Forms.PaintEventArgs e)
{
    //getIVSUIShell2
    IVsUIShell2 uiShell2 = Package.GetService(typeof(SVsUIShell)) as IVsUIShell2;
    Debug.Assert (uiShell2 != null, "failed to get IVsUIShell2");

    if (uiShell2 != null)
    {
        //get the COLORREF structure
        uint win32Color;
        uiShell2.GetVSSysColorEx((int)__VSSYSCOLOREX.VSCOLOR_SMARTTAG_HOVER_FILL, out win32Color);

        //translate it to a managed Color structure
        Color myColor = ColorTranslator.FromWin32((int)win32Color);
        //use it
        e.Graphics.FillRectangle(new SolidBrush(myColor), 0, 0, 100, 100);
    }
}
```

如果正在处理Visual Basic，请使用：

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>从 WPF UI

可以通过导出到Visual Studio 的值绑定到颜色 `ResourceDictionary` 。 下面是使用颜色表中的资源以及绑定到 XAML 中的环境字体数据的示例。

```xml
<Style TargetType="{x:Type Button}">
    <Setter Property="TextBlock.FontFamily"
            Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
    <Setter Property="TextBlock.FontSize"
            Value="{DynamicResource VsFont.EnvironmentFontSize}" />
    <Setter Property="Background"
            Value="{DynamicResource VsBrush.EnvironmentBackgroundGradient}" />
</Style>
```

#### <a name="helper-classes-and-methods-for-managed-code"></a>托管代码的帮助程序类和方法

对于托管代码，shell 的托管包框架库 () 一些帮助程序类，方便使用 `Microsoft.VisualStudio.Shell.12.0.dll` 主题颜色。

MPF 中的 类 `Microsoft.VisualStudio.Shell.VsColors` 中的帮助程序方法包括 `GetThemedGDIColor()` 和 `GetThemedWPFColor()` 。 这些帮助程序方法将主题项的颜色值返回为 `System.Drawing.Color` 或 `System.Windows.Media.Color` ，以在 WinForms 或 WPF UI 中使用。

```csharp
IVsUIShell5 shell5;
Button button = new Button();
button.BackColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemBrushKey);
button.ForeColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemTextBrushKey);

/// <summary>
/// Gets a System.Drawing.Color value from the current theme for the given color key.
/// </summary>
/// <param name="vsUIShell">The IVsUIShell5 service, used to get the color's value.</param>
/// <param name="themeResourceKey">The key to find the color for.</param>
/// <returns>The current theme's value of the named color.</returns>
public static System.Drawing.Color GetThemedGDIColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorRgba(vsUIShell, themeResourceKey);

   // Note: The Win32 color we get back from IVsUIShell5.GetThemedColor is ABGR
   return System.Drawing.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}

private static byte[] GetThemedColorRgba(IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Guid category = themeResourceKey.Category;
   __THEMEDCOLORTYPE colorType = __THEMEDCOLORTYPE.TCT_Foreground
   if (themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundColor || themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundBrush)
   {
      colorType = __THEMEDCOLORTYPE.TCT_Background;
   }

   // This call will throw an exception if the color is not found
   uint rgbaColor = vsUIShell.GetThemedColor(ref category, themeResourceKey.Name, (uint)colorType);
   return BitConverter.GetBytes(rgbaColor);
}
public static System.Windows.Media.Color GetThemedWPFColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)
{
   Validate.IsNotNull(vsUIShell, "vsUIShell");
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");

   byte[] colorComponents = GetThemedColorComponents(vsUIShell, themeResourceKey);

    return System.Windows.Media.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);
}
```

类还可用于获取给定 WPF 颜色资源键的 VSCOLOR 标识符，反之亦然。

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

类的方法 `VsColors` 查询 VSColor 服务，以每次调用它们时返回颜色值。 若要获取作为 的颜色值，另一种性能更好的替代方法是改为使用 类的方法，这些方法缓存从 `System.Drawing.Color` `Microsoft.VisualStudio.PlatformUI.VSThemeColor` VSColor 服务获取的颜色值。 类在内部订阅 shell 广播消息事件，并放弃发生主题更改事件时缓存的值。 此外， 类提供 。订阅主题更改的 NET 友好事件。 使用 `ThemeChanged` 事件添加新处理程序，并使用 `GetThemedColor()` 方法获取感兴趣的 的颜色 `ThemeResourceKeys` 值。 示例代码可能如下所示：

```csharp
public MyWindowPanel()
{
    InitializeComponent();

    // Subscribe to theme changes events so we can refresh the colors
    VSColorTheme.ThemeChanged += VSColorTheme_ThemeChanged;

    RefreshColors();
}

private void VSColorTheme_ThemeChanged(ThemeChangedEventArgs e)
{
    RefreshColors();

    // Also post a message to all the children so they can apply the current theme appropriately
    foreach (System.Windows.Forms.Control child in this.Controls)
    {
        NativeMethods.SendMessage(child.Handle, e.Message, IntPtr.Zero, IntPtr.Zero);
    }
}

private void RefreshColors()
{
    this.BackColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowBackgroundColorKey);
    this.ForeColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowTextColorKey);
}

protected override void Dispose(bool disposing)
{
    if (disposing)
    {
        VSColorTheme.ThemeChanged -= this.VSColorTheme_ThemeChanged;
        base.Dispose(disposing);}
}
```

## <a name="choosing-high-contrast-colors"></a><a name="BKMK_ChoosingHighContrastColors"></a> 选择高对比度颜色

### <a name="overview"></a>概述

Windows多个高对比度系统级主题，提高文本、背景和图像的颜色对比度，使元素在屏幕上更加不同。 出于辅助功能原因，用户切换到Visual Studio主题时，接口元素高对比度正确响应。

只有少量系统颜色可用于高对比度主题。 选择系统颜色名称时，请记住以下提示：

- **选择语义含义与要** 着色的元素相同的系统颜色。 例如，如果要为窗口中的文本选择高对比度颜色，请使用 WindowText 而不是 ControlText。

- **同时选择前景色/** 背景对，否则你将不会确信颜色选择在所有主题高对比度工作。

- **确定 UI 最重要的部分，并确保内容区域突出。** 你会丢失很多细节，颜色色调的细微差异通常会区分，因此使用强边框颜色是定义内容区域时常用的，因为不同内容区域没有颜色变体。

### <a name="system-color-set"></a>系统颜色集

WPF [团队博客：SystemColors 参考](/archive/blogs/wpf/systemcolors-reference) 中的表指示系统颜色名称的完整集，以及每个主题中显示的相应色调。

将这组有限的颜色应用于 UI 时，预期会丢失"正常"主题 中呈现的 *细微细节*。 下面是具有细微灰色的 UI 示例，用于区分工具窗口中的区域。 与模式中显示的相同窗口高对比度，可以看到所有背景都具有相同的色调，并且这些区域边框单独由边框指示：

![如何在数据中丢失细微高对比度](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />如何在数据中丢失细微高对比度

#### <a name="choosing-text-colors-in-an-editor"></a>在编辑器中选择文本颜色

着色文本在编辑器或设计图面上用于指示含义，例如，允许轻松识别相似项组。 但在高对比度主题中，无法区分三种以上文本颜色。 WindowText、GrayText 和 HotTrackText 是唯一可用于 WindowBackground 图面的颜色。 由于不能使用三种以上颜色，因此请仔细选择要在启用模式时显示高对比度差异。

编辑器图面上允许的每个标记名称的色调，因为它们显示在每个标记高对比度主题：

![高对比度编辑器比较](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />高对比度编辑器比较

蓝色主题中的编辑器图面示例：

![蓝色主题中的编辑器](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />蓝色主题中的编辑器

![主题中的高对比度 #1编辑器](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />主题中的高对比度 #1编辑器

### <a name="usage-patterns"></a>使用模式

许多常见的 UI 元素已定义了高对比度颜色。 在选择自己的系统颜色名称时，可以引用这些使用模式，以便 UI 元素与类似的组件保持一致。

| 系统颜色 | 使用情况 |
| --- | --- |
| ActiveCaption | - 活动 IDE 和悬停窗口按钮符号，然后按<br />- IDE 和排长窗口的标题栏背景<br />- 默认状态栏背景 |
| ActiveCaptionText | - 活动 IDE 和标题栏前景色窗口 (文本和字形) <br />- 悬停时活动窗口按钮的背景和边框，然后按 |
| 控件 | - 组合框、下拉列表和搜索控件默认和禁用背景，包括下拉按钮<br />- 停靠目标按钮背景<br />- 命令栏背景<br />- 工具窗口背景 |
| ControlDark | - IDE 背景<br />- 菜单和命令栏分隔符<br />- 命令栏边框<br />- 菜单阴影<br />- 默认工具窗口选项卡，并悬停边框和分隔符<br />- 文档井溢出按钮背景<br />- 停靠目标字形边框 |
| ControlDarkDark |- 未聚焦的选定文档选项卡窗口 |
| ControlLight |- 自动隐藏选项卡边框<br />- 组合框和下拉列表边框<br />- 停靠目标背景和边框 |
| ControlLightLight | - 选定、聚焦的边框 |
| ControlText | - 组合框和下拉列表字形<br />- 工具窗口未选择选项卡文本 |
| GrayText |- 组合框和下拉列表禁用边框、下拉字形、文本和菜单项文本<br />- 已禁用菜单文本<br />- 搜索控件"搜索选项"标头文本<br />- 搜索控件节分隔符 |
| 突出显示 | - 所有悬停和按下的背景和边框，组合框下拉按钮背景和文档井溢出按钮边框除外<br />- 选定的项背景 |
| HighlightText | - 所有悬停和按下的前景 (文本和字形) <br />- 聚焦的工具窗口和文档选项卡窗口控制前景<br />- 聚焦的工具窗口标题栏边框<br />- 聚焦、选定的"临时"选项卡前景<br />- 悬停并按文档井溢出按钮边框<br />- 选定的图标边框|
| HotTrack | - 按下时滚动条滚动块背景和边框<br />- 按下时滚动条箭头字形 |
| InactiveCaption | - 悬停时处于非活动状态的 IDE 和窗口按钮符号<br />- IDE 和排长窗口的标题栏背景<br />- 禁用的搜索控件背景 |
| InactiveCaptionText | - 非活动 IDE 和四边形窗口标题栏 (文本和字形) <br />- 鼠标悬停时的非活动窗口按钮背景和边框<br />- 未聚焦的工具窗口按钮背景和边框<br />-已禁用搜索控制前景 |
| 菜单 | -下拉菜单背景<br />-选中并禁用选中标记背景 |
| MenuText | -下拉菜单边框<br />-复选标记<br />-菜单字形<br />-下拉菜单文本<br />-选定的图标边框 |
| Scrollbar | -滚动条和滚动条箭头背景，所有状态 |
| 窗口 | -自动隐藏选项卡背景<br />-菜单栏和命令架背景<br />-"打开" 和 "临时" 选项卡的 "失去焦点" 或 "未选定文档" 窗口选项卡背景和文档边框<br />-失去焦点工具窗口标题栏背景<br />-工具窗口选项卡背景，已选中和未选择 |
| WindowFrame | -IDE 边框 |
| WindowText | -自动隐藏选项卡前景<br />-选定的工具窗口选项卡前景<br />-失去焦点 "文档窗口" 选项卡和 "失去焦点" 或未选定的临时选项卡前景<br />-树形视图默认前景并悬停在未选定的标志符号上<br />-工具窗口选定的选项卡边框<br />-滚动条缩略背景、边框和字形 |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a> 公开最终用户的颜色

### <a name="overview"></a>概述

有时，您需要允许最终用户自定义您的 UI，就像您在创建代码编辑器或设计图面时。 要执行此操作，最常见的方法是使用 " **工具 &gt; 选项** " 对话框。 除非您的 UI 需要特殊的控件，否则提供自定义的最简单方法是通过对话框的 "**环境**" 部分中的 "**字体和颜色**" 页。 对于为自定义公开的每个元素，用户都可以选择更改前景色、背景色或同时更改两者。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>为可自定义的颜色生成 VSPackage

VSPackage 可以通过自定义类别和 "字体和颜色" 属性页上的 "显示项目" 来控制字体和颜色。 使用此机制时，Vspackage 必须实现 [IVsFontAndColorDefaultsProvider](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider) 接口及其关联接口。

原则上，此机制可用于修改所有现有显示项以及包含它们的类别。 但是，它不应用于修改 "文本编辑器" 类别或其显示项。 有关 "文本编辑器" 类别的详细信息，请参阅 " [字体和颜色概述](/previous-versions/visualstudio/visual-studio-2015/extensibility/font-and-color-overview?preserve-view=true&view=vs-2015)"。

若要实现自定义类别或显示项，VSPackage 必须：

- **在注册表中创建或标识类别。** IDE 的 " **字体和颜色** " 属性页的实现将使用此信息来正确查询支持给定类别的服务。

- **在注册表中创建或标识组 (可选) 。** 定义组（表示两个或多个类别的联合）可能会很有用。 如果定义了组，则 IDE 会自动合并子类别，并在组内分配显示项。

- **实现 IDE 支持。**

- **处理字体和颜色更改。**

#### <a name="to-create-or-identify-categories"></a>创建或标识类别

构造一种特殊类型的类别注册表项， `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]` 其中， `<Category>` 是该类别的非本地化名称。

用两个值填充注册表：

| 名称 | 类型 | 数据 | 说明 |
| --- | --- | --- | --- |
| Category | REG_SZ | GUID | 为标识类别而创建的 GUID |
| 包裹 | REG_SZ | GUID | 支持该类别的 VSPackage 服务的 GUID |

 注册表中指定的服务必须为相应的类别提供 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 的实现。

#### <a name="to-create-or-identify-groups"></a>创建或标识组

构造一种特殊类型的类别注册表项， `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]` 其中， `<group>` 是组的非本地化名称。

用两个值填充注册表：

| 名称 | 类型 | 数据 | 说明 |
|--- | --- | --- | --- |
| Category | REG_SZ | GUID | 为标识类别而创建的 GUID |
| 包裹 | REG_SZ | GUID | 支持该类别的 VSPackage 服务的 GUID |

注册表中指定的服务必须 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 为相应组提供的实现。

![IVsFontAndColorGroup 的实现](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />`IVsFontAndColorGroup` 的实现

### <a name="to-implement-ide-support"></a>实现 IDE 支持

实现[GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)，这将为提供[](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 每个类别或组 GUID 返回 IVsFontAndColorDefaults 接口或 IDE 接口。

对于它支持的每个类别，VSPackage 实现了 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 接口的单独实例。

通过 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 实现的方法必须为 IDE 提供以下内容：

- 类别中显示项的列表

- 显示项的可本地化名称

- 显示类别中每个成员的信息

> [!NOTE]
> 每个类别都必须至少包含一个显示项。

IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 接口来定义多个类别的联合。

它的实现为 IDE 提供了：

- 构成给定组的类别的列表

- 访问支持组中的每个类别的 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 实例

- 可本地化组名称

#### <a name="updating-the-ide"></a>更新 IDE

IDE 缓存有关字体和颜色设置的信息。 因此，在对 IDE 字体和颜色配置进行修改后，确保缓存是最新的，这是最佳做法。

更新缓存是通过 [IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) 接口完成的，可以全局执行，也可以仅在所选项目上执行。

### <a name="handling-font-and-color-changes"></a>处理字体和颜色更改

若要正确支持 VSPackage 显示的文本的着色，支持 VSPackage 的着色服务必须响应用户通过 "字体和颜色" 属性页所做的更改。

为此，VSPackage 必须：

- 通过实现 [IVsFontAndColorEvents](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents)接口 **处理 IDE 生成的事件**。 在用户修改 "字体和颜色" 页后，IDE 将调用相应的方法。 例如，如果选择新字体，它将调用 [OnFontChanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged) 方法。

  **或者**

- **轮询 IDE 中的更改**。 可以通过系统实现的 [以下](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) 接口完成此操作。 尽管主要是为了支持暂留，但 [GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem) 方法可以获取显示项的字体和颜色信息。 有关字体和颜色设置的详细信息，请参阅 MSDN 文章[访问存储的字体和颜色设置](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-stored-font-and-color-settings?preserve-view=true&view=vs-2015)。

> [!NOTE]
> 若要确保轮询结果正确，请使用 [IVsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) 接口来确定是否需要缓存刷新和更新，然后再调用 [以下](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) 接口的检索方法。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>在不实现接口的情况下注册自定义字体和颜色类别

下面的代码示例演示如何在不实现接口的情况下注册自定义字体和颜色类别：

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

对于此代码示例：

- `"NameID"` = 包中本地化类别名称的资源 ID
- `"ToolWindowPackage"` = 包 GUID
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"` 只是一个示例，实际值可以是由实施者提供的新 GUID。

### <a name="set-the-font-and-color-property-category-guid"></a>设置 "字体和颜色" 属性类别 GUID

下面的代码示例演示如何设置类别 Guid。

```csharp
// m_pView is your IVsTextView
IVsTextEditorPropertyCategoryContainer spPropCatContainer =
(IVsTextEditorPropertyCategoryContainer)m_pView;
if (spPropCatContainer != null)
{
IVsTextEditorPropertyContainer spPropContainer;
Guid GUID_EditPropCategory_View_MasterSettings =
new Guid("{D1756E7C-B7FD-49a8-B48E-87B14A55655A}");
hr = spPropCatContainer.GetPropertyCategory(
ref GUID_EditPropCategory_View_MasterSettings,
out spPropContainer);
if(hr == 0)
{
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_FontCategory,
catGUID);
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_ColorCategory,
catGUID);
}
}
```
