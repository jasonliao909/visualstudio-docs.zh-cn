---
title: Visual Studio 的颜色和样式 |Microsoft Docs
description: 了解 Visual Studio 的用户体验如何使用颜色作为通信工具，而不是完全美观的原因。
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
ms.openlocfilehash: 9285e13e2f413ab2cc2e04be11ebe1ece3b04c25
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122028600"
---
# <a name="colors-and-styling-for-visual-studio"></a>Visual Studio 的颜色和样式

## <a name="use-color-in-visual-studio"></a>在 Visual Studio 中使用颜色

在 Visual Studio 中，颜色主要用作一种通信工具，而不是作为装饰。 如果要执行以下操作，请尽量少使用颜色并保留它：

- 传达含义或从属 (例如，平台或语言修饰符) 

- 请注意 (例如，指示状态更改) 

- 提高可读性并提供用于导航 UI 的特征点

- 增加性能

有多个选项可用于在 Visual Studio 中为 UI 元素分配颜色。 有时，很难确定你应该使用哪种选项，或是如何正确使用它。 本主题将帮助你：

- 了解用于在 Visual Studio 中定义颜色的不同服务和系统。

- 为给定元素选择正确的选项。

- 正确使用您选择的选项。

> [!NOTE]
> 切勿在 UI 元素中硬编码十六进制、RGB 或系统颜色。 使用服务可灵活地调整色调。 此外，如果没有该服务，将无法利用 [VSColor 服务](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService)的主题切换功能。

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>向 Visual Studio 接口元素分配颜色的方法

选择最适合您的 UI 元素的方法。

| 你的 UI | 方法 | 分别是哪两个参数？ |
| --- | --- | --- |
| 您具有嵌入的或独立的对话框。 | **系统颜色** | 允许操作系统定义 UI 元素的颜色和外观的系统名称，如通用对话框控件。 |
| 你具有要与整个 VS 环境一致的自定义 UI，并且你具有与共享令牌的类别和语义含义相匹配的 UI 元素。 | **公共共享颜色** | 特定 UI 元素的现有预定义颜色标记名称 |
| 您有一项功能或一组功能，但对于类似元素没有共享的颜色。 | **自定义颜色** | 特定于区域的颜色标记名称，不应与其他 UI 共享 |
| 您希望允许最终用户自定义 UI 或内容 (例如，对于文本编辑器或专用设计器 windows) 。 | **最终用户自定义**<br /><br />**(工具 &gt; 选项 "对话框)** | 设置在 "**工具 &gt; 选项**" 对话框的 "字体和颜色" 页中定义，或在特定于一个 UI 功能的专用页中定义。 |

### <a name="visual-studio-themes"></a>Visual Studio 主题

Visual Studio 特性三个不同的颜色主题：浅、暗和蓝色。 它还检测高对比度模式，这是为辅助功能而设计的系统范围的颜色主题。

在首次使用 Visual Studio 时，系统将提示用户选择一个主题，并能够在以后通过转到 "**工具选项" "环境" " &gt; &gt; &gt; 常规**" 并从 "颜色主题" 下拉菜单中选择一个新主题来切换主题。

用户还可以使用 "控制面板" 将其整个系统切换为多个高对比度主题之一。 如果用户选择高对比度主题，则 Visual Studio 颜色主题选择器将不再影响 Visual Studio 中的颜色，但当用户退出高对比度模式时，会保存任何主题更改。 有关高对比度模式的详细信息，请参阅 [选择高对比度颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors)。

### <a name="the-vscolor-service"></a>VSColor 服务

Visual Studio 提供了一种称为 VSColor service 的环境颜色服务，该服务允许你将 UI 元素的颜色值绑定到包含每个 Visual Studio 主题的颜色值的命名条目。 这可确保颜色会自动更改，以反映当前用户选择的主题或系统高对比度模式。 使用服务意味着在一个位置处理所有与主题相关的颜色更改的实现，并且如果你使用的是服务中的常见共享颜色，你的 UI 会自动反映 Visual Studio 的将来版本中的新主题。

### <a name="implementation"></a>实现

Visual Studio 源代码包含多个包定义文件，其中包含每个主题的标记名称和各自颜色值的列表。 颜色服务将读取在这些包定义文件中定义的 VSColors。 这些颜色在 XAML 标记或代码中引用，然后通过 `IVsUIShell5.GetThemedColor` 方法或 DynamicResource 映射进行加载。

### <a name="system-colors"></a>系统颜色

默认情况下，公共控件引用系统颜色。 如果希望 UI 使用系统颜色，如创建嵌入或独立对话框时，无需执行任何操作。

### <a name="common-shared-colors-in-the-vscolor-service"></a>VSColor 服务中的常见共享颜色

接口元素应该反映总体 Visual Studio 的环境。 通过重复使用适用于你正在设计的 UI 组件的常见共享颜色，你可以确保你的接口与其他 Visual Studio 接口一致，并且你的颜色将在添加或更新主题时自动更新。

使用常见的共享颜色之前，请确保了解如何正确使用它们。 不正确地使用常见的共享颜色可能会导致用户遇到不一致、令人费解或混乱的体验。

### <a name="user-customizable-colors"></a>用户可自定义的颜色

请参阅： [公开最终用户的颜色](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

有时，您需要允许最终用户自定义您的 UI，就像您创建代码编辑器或设计图面一样。 可以在 "**工具 &gt; 选项**" 对话框的 "**字体和颜色**" 部分中找到可自定义的 UI 组件，用户可以在其中选择更改前景色、背景色或同时更改两者。

!["工具 &gt; 选项" 对话框](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />"工具 &gt; 选项" 对话框

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a> VSColor 服务

Visual Studio 提供环境颜色服务，也称为 VSColor 服务或 shell color 服务。 此服务允许你将 UI 元素的颜色值绑定到一个名称-值颜色集，其中包含每个主题的颜色。 VSColor 服务必须用于所有 UI 元素，因此，颜色会自动更改以反映当前用户选择的主题，这样，绑定到环境颜色服务的 UI 会与未来版本的 Visual Studio 中的新主题集成。

### <a name="how-the-service-works"></a>服务的工作原理

环境颜色服务会在 .pkgdef 中为 UI 组件读取 VSColors 定义的内容。 然后，在 XAML 标记或代码中引用这些 VSColors，并通过 `IVsUIShell5.GetThemedColor` 或映射进行加载 `DynamicResource` 。

![环境颜色服务体系结构](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />环境颜色服务体系结构

### <a name="accessing-the-service"></a>访问服务

有多种不同的方法可用于访问 VSColor 服务，具体取决于所使用的颜色标记的类型以及所使用的代码类型。

#### <a name="predefined-environment-colors"></a>预定义环境颜色

##### <a name="from-native-code"></a>从本机代码

Shell 提供提供对颜色的访问的服务 `COLORREF` 。 服务/接口为：

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

在文件 VSShell80 中，枚举 `__VSSYSCOLOREX` 具有 shell 颜色常量。 若要使用它，请将作为索引值传入 MSDN 中所述的一个值， `enum __VSSYSCOLOREX` 或者作为 Windows 系统 API 接受的常规索引号传入 `GetSysColor` 。 这样做会返回应在第二个参数中使用的颜色的 RGB 值。

如果使用新颜色存储笔或画笔，则必须在 `AdviseBroadcastMessages` Visual Studio shell)  (，并侦听 `WM_SYSCOLORCHANGE` 和 `WM_THEMECHANGED` 消息。

若要访问本机代码中的颜色服务，请调用，如下所示：

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> `COLORREF`返回的值 `GetVSSysColorEx()` 只包含 R、G、B 主题颜色的组成部分。 如果主题条目使用透明度，则会在返回前丢弃 alpha 通道值。 因此，如果需要在透明通道非常重要的地方使用所需的环境颜色，则应使用 `IVsUIShell5.GetThemedColor` 而不是 `IVsUIShell2::GetVSSysColorEx` ，如本主题后面所述。

##### <a name="from-managed-code"></a>从托管代码

通过本机代码访问 VSColor 服务非常简单。 但是，如果您正在处理托管代码，则确定如何使用服务可能比较棘手。 考虑到这一点，以下是演示此过程的 c # 代码片段：

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

如果使用的是 Visual Basic，请使用：

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>从 WPF UI

可以通过导出到应用程序中的值绑定到 Visual Studio 颜色 `ResourceDictionary` 。 下面是一个示例，介绍如何使用颜色表中的资源，以及如何绑定到 XAML 中的环境字体数据。

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

对于托管代码，shell 的托管包框架库 (`Microsoft.VisualStudio.Shell.12.0.dll`) 包含几个帮助器类，以方便使用主题颜色。

MPF 中类的帮助器方法 `Microsoft.VisualStudio.Shell.VsColors` 包括 `GetThemedGDIColor()` 和 `GetThemedWPFColor()` 。 这些帮助器方法将主题条目的颜色值作为 `System.Drawing.Color` 或返回 `System.Windows.Media.Color` ，以在 WINFORMS 或 WPF UI 中使用。

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

类的方法 `VsColors` 查询 VSColor 服务，以便每次调用时返回颜色值。 若要获取的颜色值为 `System.Drawing.Color` ，使用更好性能的一种替代方法是改用类的方法 `Microsoft.VisualStudio.PlatformUI.VSThemeColor` ，这会缓存从 VSColor 服务获取的颜色值。 类在内部订阅以 shell 广播消息事件，并在发生主题更改事件时丢弃缓存的值。 此外，类还提供。用于订阅主题更改的网络友好事件。 使用 `ThemeChanged` 事件可添加新的处理程序，并使用 `GetThemedColor()` 方法获取相关的颜色值 `ThemeResourceKeys` 。 示例代码可能如下所示：

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

Windows 使用多个高对比度系统级主题，这些主题提高了文本、背景和图像的颜色对比度，使元素在屏幕上显得更加独特。 出于辅助功能的原因，当用户切换到高对比度主题时，Visual Studio 接口元素能正确响应，这一点很重要。

只有少量的系统颜色可用于高对比度主题。 选择系统颜色名称时，请记住以下提示：

- 选择与您要着色的元素 **具有相同语义含义的系统颜色**。 例如，如果为窗口中的文本选择高对比度的颜色，请使用 WindowText 而不是 ControlText。

- 同时 **选择前景/背景对**，也不会确信您的颜色选择在所有高对比度主题中都有效。

- **确定 UI 的哪些部分是最重要的部分，并确保内容区域将会突出。** 您将会丢失很多详细信息，颜色色相的细微差异通常会区分开来，因此使用强边框颜色是定义内容区域的常用方法，因为不同的内容区域没有任何颜色变体。

### <a name="system-color-set"></a>系统颜色集

[WPF 团队博客上的表： SystemColors 引用](/archive/blogs/wpf/systemcolors-reference)指示一组完整的系统颜色名称，以及每个主题中显示的相应色相。

将此有限的一组颜色应用于您的 UI 时， *您将会丢失 "正常" 主题中存在的细微细节*。 下面是一个使用细小灰色颜色的 UI 示例，用于区分工具窗口内的区域。 当与高对比度模式下显示的同一窗口配对时，您可以看到所有背景都具有相同的色调，并且这些区域的边框仅由边框表示：

![如何在高对比度中丢失微妙细节的示例](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />如何在高对比度中丢失微妙细节的示例

#### <a name="choosing-text-colors-in-an-editor"></a>在编辑器中选择文本颜色

着色文本在编辑器或设计图面上用于指示含义，如允许轻松识别相似项的组。 但是，在高对比度主题中，您不能区分三个以上的文本颜色。 WindowText、GrayText 和 HotTrackText 是 WindowBackground 表面上唯一可用的颜色。 由于不能使用三种以上的颜色，因此在高对比度模式下，请仔细选择要显示的最重要的差异。

编辑器表面上所允许的每个令牌名称的色相，因为它们显示在每个高对比度主题中：

![高对比度编辑器比较](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />高对比度编辑器比较

蓝色主题中的编辑器表面示例：

![蓝色主题中的编辑器](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />蓝色主题中的编辑器

![高对比度 #1 主题中的编辑器](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />高对比度 #1 主题中的编辑器

### <a name="usage-patterns"></a>使用模式

许多常见 UI 元素已经定义高对比度颜色。 选择自己的系统颜色名称时，可以引用这些使用模式，以便您的 UI 元素与类似的组件一致。

| 系统颜色 | 使用情况 |
| --- | --- |
| ActiveCaption | -悬停并按下时的活动 IDE 和 rafted 窗口按钮字形<br />-IDE 和 rafted 窗口的标题栏背景<br />-默认状态栏背景 |
| ActiveCaptionText | -用于标题栏前景 (文本和字形的活动 IDE 和 rafted 窗口) <br />-悬停并按下活动窗口按钮的背景和边框 |
| 控件 | -组合框、下拉列表和搜索控件默认和禁用的背景，包括下拉按钮<br />-"停靠目标" 按钮背景<br />-命令栏背景<br />-工具窗口背景 |
| ControlDark | -IDE 背景<br />-菜单和命令栏分隔符<br />-命令栏边框<br />-菜单阴影<br />-工具窗口选项卡默认和悬停边框和分隔符<br />-"文档溢出" 按钮背景<br />-停靠目标标志符号边框 |
| ControlDarkDark |-失去焦点，选择的文档选项卡窗口 |
| ControlLight |-自动隐藏选项卡边框<br />-组合框和下拉列表边框<br />-停靠目标背景和边框 |
| ControlLightLight | -选定，重点临时边框 |
| ControlText | -组合框和下拉列表标志符号<br />-未选定的工具窗口选项卡文本 |
| GrayText |-组合框和下拉列表禁用边框、下拉标志符号、文本和菜单项文本<br />-已禁用菜单文本<br />-搜索控件 "搜索选项" 标头文本<br />-搜索控件节分隔符 |
| 突出显示 | -所有悬停和按下的背景和边框（组合框下拉按钮的背景和文档溢出按钮边框除外）<br />-选定的项背景 |
| HighlightText | -所有悬停并按下的 foregrounds (文本和字形) <br />重点工具窗口和文档选项卡窗口控件前景<br />重点工具窗口标题栏边框<br />-专注于选定的临时选项卡前景<br />-悬停并按下时的文档溢出按钮边框<br />-选定的图标边框|
| HotTrack | -按下滚动条的滚动条的背景和边框<br />-按下的滚动条箭头标志符号 |
| InactiveCaption | -悬停时的非活动 IDE 和 rafted 窗口按钮字形<br />-IDE 和 rafted 窗口的标题栏背景<br />-已禁用搜索控件背景 |
| InactiveCaptionText | -非活动 IDE 和 rafted windows 标题栏前台 (文本和字形) <br />-悬停时的非活动窗口按钮背景和边框<br />-失去焦点工具窗口按钮的背景和边框<br />- 禁用的搜索控件前景 |
| 菜单 | - 下拉菜单背景<br />- 已选中和禁用的选中标记背景 |
| MenuText | - 下拉菜单边框<br />- 选中标记<br />- 菜单字形<br />- 下拉菜单文本<br />- 选定的图标边框 |
| Scrollbar | - 滚动条和滚动条箭头背景，所有状态 |
| 窗口 | - 自动隐藏选项卡背景<br />- 菜单栏和命令架背景<br />- 未聚焦或未选择的文档窗口选项卡背景和文档边框，适用于打开选项卡和临时选项卡<br />- 未聚焦的工具窗口标题栏背景<br />- "工具窗口"选项卡背景（已选中和未选中） |
| WindowFrame | - IDE 边框 |
| WindowText | - 自动隐藏选项卡前景<br />- 选定的工具窗口选项卡前景<br />- 未聚焦的文档窗口选项卡和未聚焦或未选择的临时选项卡前景<br />- 树视图默认前景，将鼠标悬停在未选择字形上<br />- 工具窗口已选择选项卡边框<br />- 滚动条滚动条背景、边框和字形 |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a> 向最终用户公开颜色

### <a name="overview"></a>概述

有时，需要允许最终用户自定义 UI，就像创建代码编辑器或设计图面时一样。 为此，最常见的方法为使用"工具选项 **&gt; "** 对话框。 除非具有需要特殊控件的高度专用 UI，否则显示自定义项的最简单方法是通过对话框的"环境"部分内的"字体和 **颜色**"页。  对于公开用于自定义的每个元素，用户可以选择更改前景色和/或背景色。

### <a name="building-a-vspackage-for-your-customizable-colors"></a>为可自定义的颜色生成 VSPackage

VSPackage 可以通过自定义类别控制字体和颜色，并显示"字体和颜色"属性页上的项。 使用此机制时，VSPackages 必须实现 [IVsFontAndColorDefaultsProvider](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider) 接口及其关联的接口。

从原理上来说，此机制可用于修改所有现有显示项以及包含这些项的类别。 但是，它不应用于修改"文本编辑器"类别或其显示项。 有关"文本编辑器"类别详细信息，请参阅 [字体和颜色概述](/previous-versions/visualstudio/visual-studio-2015/extensibility/font-and-color-overview?preserve-view=true&view=vs-2015)。

若要实现自定义类别或显示项，VSPackage 必须：

- **在注册表中创建或标识类别。** IDE 的"字体和颜色"属性页的实现使用此信息正确查询支持给定类别的服务。

- **在注册表中创建或标识组 (可选) 。** 定义表示两个或多个类别的并组的组可能很有用。 如果定义了组，IDE 会自动合并子类别，并分发该组内的显示项。

- **实现 IDE 支持。**

- **处理字体和颜色更改。**

#### <a name="to-create-or-identify-categories"></a>创建或标识类别

在 下构造一种特殊类型的类别注册表项，其中 是类别的非 `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]` `<Category>` 本地化名称。

使用两个值填充注册表：

| 名称 | 类型 | 数据 | 说明 |
| --- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 为标识类别而创建的 GUID |
| 包裹 | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

 注册表中指定的服务必须提供相应类别的 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 的实现。

#### <a name="to-create-or-identify-groups"></a>创建或标识组

在 下构造一种特殊类型的类别注册表项，其中 是组 `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]` `<group>` 的非本地化名称。

使用两个值填充注册表：

| 名称 | 类型 | 数据 | 说明 |
|--- | --- | --- | --- |
| 类别 | REG_SZ | GUID | 为标识类别而创建的 GUID |
| 包裹 | REG_SZ | GUID | 支持类别的 VSPackage 服务的 GUID |

注册表中指定的服务必须为相应的组 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 提供 的实现。

![IVsFontAndColorGroup 的实现](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />`IVsFontAndColorGroup` 的实现

### <a name="to-implement-ide-support"></a>实现 IDE 支持

实现 [GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject)，它返回提供的每个类别或组 GUID 的 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 接口或 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> IDE 接口。

对于它支持的每一个类别，VSPackage 实现 [IVsFontAndColorDefaults 接口的单独](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 实例。

通过 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 实现的方法必须为 IDE 提供：

- 类别中显示项的列表

- 显示项的可本地化名称

- 显示类别的每个成员的信息

> [!NOTE]
> 每个类别必须至少包含一个显示项。

IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> 接口定义多个类别的联合。

它的实现为 IDE 提供：

- 包含给定组的类别列表

- 访问支持组内每个类别的 [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) 实例

- 可本地化的组名称

#### <a name="updating-the-ide"></a>更新 IDE

IDE 缓存有关字体和颜色设置的信息。 因此，在修改 IDE 字体和颜色配置后，最佳做法是确保缓存是最新的。

通过 [IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) 接口更新缓存，可以全局执行，也可以仅对选定项执行。

### <a name="handling-font-and-color-changes"></a>处理字体和颜色更改

若要正确支持 VSPackage 显示的文本着色，支持 VSPackage 的着色服务必须响应用户通过"字体和颜色"属性页发起的更改。

为此，VSPackage 必须：

- **通过实现** [IVsFontAndColorEvents](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents) 接口来处理 IDE 生成的事件。 IDE 在用户修改"字体和颜色"页后调用适当的方法。 例如，如果选择新字体，则调用 [OnFontChanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged) 方法。

  **或者**

- **轮询 IDE 的更改**。 这可以通过系统实现的 [IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) 接口完成。 虽然主要用于支持持久性， [但 GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem) 方法可以获取显示项的字体和颜色信息。 有关字体和颜色设置详细信息，请参阅 MSDN 文章[访问存储的字体和颜色设置。](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-stored-font-and-color-settings?preserve-view=true&view=vs-2015)

> [!NOTE]
> 若要确保轮询结果正确，请使用 [IVsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) 接口在调用 [IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) 接口的检索方法之前确定是否需要缓存刷新和更新。

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>注册自定义字体和颜色类别而不实现接口

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
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"` 只是一个示例，实际值可以是实现者提供的新 GUID。

### <a name="set-the-font-and-color-property-category-guid"></a>设置"字体和颜色"属性类别 GUID

下面的代码示例演示如何设置类别 GUID。

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
