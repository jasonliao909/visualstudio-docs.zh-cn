---
title: 字体和格式设置Visual Studio |Microsoft Docs
description: 了解为应用设计的新功能的字体和Visual Studio，包括如何使用环境字体。
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e6e26b18c838fc240d7fab398f8626890eed0d31
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901677"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Visual Studio 的字体和格式
## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a> 环境字体
 所有字体Visual Studio必须公开给用户进行自定义。 这主要通过"工具""选项"对话框中 **的** "字体和颜色 **>完成** 。 字体设置的三个主要类别是：

- **环境字体** - 集成开发 (IDE 的主要字体) ，用于所有界面元素，包括对话框、菜单、工具窗口和文档窗口。 默认情况下，环境字体绑定到在当前版本的 Windows 中显示为 9 pt Segoe UI的系统字体。 将一个字体用于所有接口元素有助于确保整个 IDE 中的字体外观一致。

- **文本编辑器** - 可以在"工具"和"选项"的"文本编辑器"页中自定义 **代码和其他>元素**。

- **特定集合** - 提供用户自定义其界面元素的设计器窗口可能会公开特定于其设计图面的字体，该字体在"工具"和"选项"中> **页面**。

### <a name="editor-font-customization-and-resizing"></a>编辑器字体自定义和调整大小
 用户通常会根据偏好在编辑器中放大或缩放文本的大小和/或颜色，而与常规用户界面无关。 由于环境字体用于可能在编辑器/设计器内或作为编辑器/设计器的一部分显示的元素，因此，当更改其中一个字体分类时，必须注意预期的行为。

 创建显示在编辑器中但不是内容的一部分的 UI 元素时，使用环境字体而不是文本字体非常重要，以便元素以可预测的方式重设大小。

1. 对于编辑器中的代码文本，使用代码文本字体设置调整大小并响应编辑器文本的缩放级别。

2. 接口的所有其他元素都应绑定到环境字体设置，并响应环境中的任何全局更改。 这包括但不限于：

    - 上下文菜单中的文本

    - 编辑器修饰中的文本，如灯泡菜单文本、快速查找编辑器窗格和导航到窗格

    - 在对话框中标记文本，例如" **在文件中查找"** 或 **"重构"**

### <a name="accessing-the-environment-font"></a>访问环境字体
 在 Native 或 WinForms 代码中，可以通过在从服务查询接口后调用 方法来 `IUIHostLocale::GetDialogFont` 访问环境 `SID_SUIHostLocale` 字体。

 对于Windows Presentation Foundation (WPF) ，请从 shell 的 类（而不是 WPF 的 类）派生 `DialogWindow` 对话窗口 `Window` 类。

 在 XAML 中，代码如下所示：

```xaml
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>
```

代码隐藏：

```csharp
internal partial class WebConfigModificationWindow : DialogWindow
{
}
```

  (将 替换为 `Microsoft.VisualStudio.Shell.11.0` MPF dll.) 

 若要显示对话框，请对 上的 `ShowModal()` 类调用 `ShowDialog()` ""。 `ShowModal()` 在 shell 中设置正确的模式状态，确保对话框在父窗口中居中，等等。

 代码如下所示:

```csharp
MyWindow window = new MyWindow();
window.ShowModal()
```

 `ShowModal` 返回 bool？  (布尔值) 布尔值与 一起， `DialogResult` 如果需要可以使用。 如果对话框在"确定"下关闭，则返回 **值为 true。**

 如果需要显示一些非对话且托管在其自己的 中的 WPF UI，例如弹出窗口或 `HwndSource` Win32/WinForms 父窗口的 WPF 子窗口，则需要在 `FontFamily` `FontSize` WPF 元素的根元素上设置 和 。  (shell 在主窗口上设置属性，但它们不会在主窗口之后继承 `HWND`) 。 shell 提供属性可以绑定到的资源，如下所示：

```xaml
<Setter Property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter Property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />
```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a> 格式设置 (缩放/粗体) 引用
 某些对话框要求特定文本为粗体或环境字体外的大小。 以前，大于环境字体的字体被编码为 `environment font +2` ""或类似字体。 使用提供的代码片段将支持高 DPI 监视器，并确保显示文本始终以正确的大小和权重显示 (如浅色或) 。

> [!NOTE]
> 应用格式设置之前，请确保遵循文本样式 [中的指南](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle)。**

 若要缩放环境字体，请根据指示设置 TextBlock 或 Label 的样式。 正确使用每个代码片段都将生成正确的字体，包括适当的大小和权重变体。

 其中 `vsui` ""是命名空间的引用 `Microsoft.VisualStudio.Shell` ：

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色

**显示为：34** pt Segoe UI浅

::: moniker range="vs-2017"

**用于： (** 独特的) UI，如起始页中的

::: moniker-end

::: moniker range=">=vs-2019"

**用于： (** 独特的) 的 UI

::: moniker-end

**过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);
```

**XAML：** 设置 TextBlock 或 Label 的样式，如下所示。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>
```

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色
 **显示为：28** pt Segoe UI Light **Use for：** large signature dialog titles， main heading in reports

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示。

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>
```

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + Semilight
 **显示为：18** pt Segoe UI Semilight **Use for：** subheadings， titles in small and medium dialogs

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>
```

#### <a name="155-environment-font"></a>155% 环境字体
 **显示为：14** pt Segoe UI **用于文档** 井 UI 或报表的节标题

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>
```

#### <a name="133-environment-font"></a>133% 环境字体
 **显示为：12** pt Segoe UI **用于：** 签名对话框和文档井 UI 中的较小子标题

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>
```

#### <a name="122-environment-font"></a>122% 环境字体
 **显示为：11** pt Segoe UI **用于：** 签名对话框中的部分标题、树视图中的顶部节点、垂直选项卡导航

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>
```

#### <a name="environment-font--bold"></a>环境字体 + 粗体
 **显示为：** 粗体显示 9 pt Segoe UI **用于：** 签名对话框、报表和文档井 UI 中的标签和子标题

 **过程代码：** 其中 `textBlock` 是以前定义的 TextBlock， `label` 是以前定义的标签：

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);
```

 **XAML：** 设置 TextBlock 或 Label 的样式，如下所示：

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>
```

### <a name="localizable-styles"></a>可本地化样式
 在某些情况下，本地化人员需要为不同的区域设置修改字体样式，例如从东亚语言的文本中删除粗体。 若要使字体样式的本地化成为可能，这些样式必须位于 .resx 文件中。 在窗体设计器中完成此操作并仍编辑字体Visual Studio是在设计时显式设置字体样式。 尽管这会创建一个完整的字体对象，并且似乎会破坏父字体的继承，但只使用 FontStyle 属性来设置字体。

 解决方法是挂钩对话框窗体 `FontChanged` 的 事件。 在这种情况下 `FontChanged` ，请演练所有控件，并检查其字体是否设置。 如果已设置，请根据窗体的字体和控件以前的字体样式，将字体更改为新字体。 代码中的一个示例是：

```csharp
private void Form1_FontChanged(object sender, System.EventArgs e)
{
          SetFontStyles();
}

/// <summary>
/// SetFontStyles - This function will iterate all controls on a page
/// and recreate their font with the desired fontstyle.
/// It should be called in the OnFontChanged handler (and also in the constructor
/// in case the IUIService is not available so OnFontChange doesn't fire).
/// This way, when the VS shell font is given to us the controls that have
/// a different style for the font (bolded for example) will recreate their font
/// and use the VS shell font but with a style variation (bolded ...).
/// </summary>
protected void SetFontStyles()
{
     SetFontStyles(this, this, this.Font);
}

protected static void SetFontStyles(Control topControl, Control parent, Font referenceFont)
{
     foreach(Control c in parent.Controls)
     {
          if (c.Controls != null && c.Controls.Count > 0) {
               SetFontStyles(topControl, c, referenceFont);
          }
          if (c.Font != topControl.Font) {
               c.Font = new Font(referenceFont, c.Font.Style);
          }
     }
}
```

 使用此代码可保证在更新窗体的字体时，控件的字体也会更新。 还应从窗体的构造函数调用此方法，因为对话框可能无法获取 的实例， `IUIService` `FontChanged` 并且事件永远不会被启动。 挂钩 `FontChanged` 将允许对话动态选取新字体，即使对话已打开。

### <a name="testing-the-environment-font"></a>测试环境字体
 若要确保 UI 使用环境字体并符合大小设置，请打开"工具">"选项 **">"环境">"字体和颜色"，** 然后选择"显示设置："下拉菜单下的"环境字体"。

 !["工具选项"对话框中的字体 &gt; 和颜色设置](../../extensibility/ux-guidelines/media/0201-a_optionsfonts.png "0201-a_OptionsFonts")<br />"工具选项"对话框中的字体 &gt; 和颜色设置

 将字体设置为与默认值非常不同的字体。 若要明确哪些 UI 不更新，请选择具有 (如"Times New Roman"的字体) 并设置非常大的大小。 然后测试 UI 以确保它遵守环境。 下面是使用许可证对话框的示例：

 ![不遵守环境字体的 UI 文本示例](../../extensibility/ux-guidelines/media/0201-b_wrongfontdialog.png "0201-b_WrongFontDialog")<br />不遵守环境字体的 UI 文本示例

 在这种情况下，"用户信息"和"产品信息"不遵循字体。 在某些情况下，这可能是显式设计选择，但如果未将显式字体指定为红线规范的一部分，则可能是 bug。

 若要重置字体，请单击"工具""选项"下的"使用默认值 **>">">字体和颜色"。**

## <a name="text-style"></a><a name="BKMK_TextStyle"></a> 文本样式
 文本样式指的是字体大小、粗细和大小写。 有关实现指南，请参阅 [环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

### <a name="text-casing"></a>文本大小写

#### <a name="all-caps"></a>全部大写
 不要在 Visual Studio 中将所有标题或标签全部使用。

#### <a name="all-lowercase"></a>全部小写
 对于 Visual Studio 中的标题或标签，不要使用全部小写形式。

#### <a name="sentence-and-title-case"></a>句子和词首大写
 Visual Studio 中的文本应使用词首大写或句子大小写，具体取决于具体情况。

|使用词首字母大写：|使用句子 case：|
|-------------------------|----------------------------|
|对话框标题|标签|
|分组框|复选框|
|菜单项|单选按钮|
|上下文菜单项|列表框项|
|按钮|状态栏|
|表标签||
|列标题||
|工具提示||

##### <a name="title-case"></a>标题格式
 "标题大小写" 是指短语中大部分或全部单词的首字母大写的样式。 在 Visual Studio 中，"标题大小写" 用于多个项目，包括：

- **Tooltip.** 示例： "预览选定项"

- **列标头。** 示例： "系统响应"

- **菜单项。** 示例： "全部保存"

  使用词首字母大写时，以下是在何时将单词和何时变为小写的准则：

|大写|注释和示例|
|---------------|---------------------------|
|所有名词||
|所有谓词|包括 "Is" 和其他窗体 "是"|
|所有副词|包括 "大于" 和 "When"|
|所有形容词|包括 "This" 和 "This"|
|所有代词|其中包括所有格 "其" 以及 "It"、"缩写式" 和 "is" 这一代词|
|第一个和最后一个单词，与语音的部分无关||
|属于动词短语的介词|"关闭所有窗口" 或 "关闭系统"|
|首字母缩写词的所有字母|HTML、XML、URL、IDE、RGB|
|组合词中的第二个单词（如果它是名词或正确的形容词），或者单词的权重相等|交叉引用，Microsoft Microsoft 软件，读/写访问，Run-Time|

|小写|示例|
|---------------|--------------|
|组合词中的第二个单词（如果它是词性的另一个部分，或修改第一个单词的分词）|操作说明、卸载|
|文章，除非标题中的第一个词是|a、an、the|
|坐标连词|and、or、and 或|
|动词短语之外的字母包含四个或更少字符的介词|into，放入，在|
|无穷短语中使用时的 "To"|"如何格式化硬盘"|

##### <a name="sentence-case"></a>句子大小写
 句子 case 是用于写入的标准大写方法，其中只有句子的第一个词是大写的，以及任何正确名词和代词 "I"。 一般情况下，对于全球受众来说，句子案例更容易阅读，尤其是在计算机翻译内容时。 使用句子 case：

1. **状态栏消息。** 它们简单、简短，只提供状态信息。 示例： "正在加载项目文件"

2. **所有其他 UI 元素**，包括标签、复选框、单选按钮和列表框项。 示例： "选择列表中的所有项目"

### <a name="text-formatting"></a>文本格式
 Visual Studio 2013 中的默认文本格式设置由 [环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)控制。 此服务帮助确保整个 IDE 中的字体外观 (集成开发环境) ，你必须使用它来保证用户的一致体验。

 Visual Studio 字体服务使用的默认大小来自 Windows，并显示为 9 pt。

 可以将格式设置应用于环境字体。 本主题介绍使用样式的方式和位置。 有关实现的信息，请参阅 [环境字体](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont)。

#### <a name="bold-text"></a>粗体文本
 在 Visual Studio 中，粗体文本会慎用，应保留为：

- 向导中的试题标签

- 指定活动项目解决方案资源管理器

- "属性" 工具窗口中的重写值

- Visual Basic 编辑器 "下拉列表中的特定事件

- 网页文档大纲中服务器生成的内容

- 复杂对话框或设计器 UI 中的节标头

#### <a name="italics"></a>斜体
 Visual Studio 不使用斜体或粗体斜体文本。

#### <a name="color"></a>Color

- 将为 (导航和命令) 的超链接保留蓝色，不应将其用于方向。

- 更大的标题 (环境字体 x 155% 或更高的) 可用于以下目的：

  - 向 visual Studio UI 签名提供视觉吸引力

  - 若要注意特定区域

  - 从标准暗灰色/黑色环境文本颜色中提供止裂槽

- 标题中的颜色应利用现有的 Visual Studio 品牌颜色，主要为紫色 #FF68217A。

- 在标题中使用颜色时，必须遵守 [Windows 颜色准则](/windows/desktop/uxguide/vis-color)，包括对比度和其他辅助功能注意事项。

### <a name="font-size"></a>字体大小
 Visual Studio UI 设计具有更浅的外观和更多的空白。 在可能的情况下，已减少或删除了 chrome 和标题栏。 尽管信息密度是Visual Studio要求，但版式仍然很重要，强调更开放的行距以及字号和粗细的变体。

 下表包含设计详细信息和视觉对象示例，这些字体用于Visual Studio。 某些显示字体变体将大小和权重（如 Semilight 或 Light）编码到其外观中。

 可在格式设置中找到所有显示字体的实现代码片段 ([缩放/粗体) 引用](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)。

#### <a name="375-environment-font--light"></a>375% 环境字体 + 浅色

|使用情况|外观|
|-|-|
|**用法：** 罕见。 仅唯一品牌 UI。<br /><br /> **执行：**<br /><br /> - 使用句子大小写<br />- 始终使用轻型<br /><br /> **不要：**<br /><br /> - 用于签名 UI（如起始页）外的其他 UI<br />- 粗体、italic 或粗体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：34** pt Segoe UI浅<br /><br /> **视觉对象示例：**<br /><br /> *当前未使用。可以在 2017 Visual Studio页中使用。*|

#### <a name="310-environment-font--light"></a>310% 环境字体 + 浅色

::: moniker range="vs-2017"

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> - 签名对话框中的较大标题<br />- 主报表标题<br /><br /> **执行：**<br /><br /> - 使用句子大小写<br />- 始终使用轻型<br /><br /> **不要：**<br /><br /> - 用于签名 UI（如起始页）外的其他 UI<br />- 粗体、italic 或粗体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：28** pt Segoe UI Light<br /><br /> **视觉对象示例：**<br /><br /> ![310% 环境字体&#43;浅色标题的示例](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

::: moniker range=">=vs-2019"

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> - 签名对话框中的较大标题<br />- 主报表标题<br /><br /> **执行：**<br /><br /> - 使用句子大小写<br />- 始终使用轻型<br /><br /> **不要：**<br /><br /> - 用于签名 UI 而不是 UI<br />- 粗体、italic 或粗体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：28** pt Segoe UI Light<br /><br /> **视觉对象示例：**<br /><br /> ![310% 环境字体&#43;浅色标题的示例](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

#### <a name="200-environment-font--semilight"></a>200% 环境字体 + Semilight

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> - 子标题<br />- 中小对话框中的标题<br /><br /> **执行：**<br /><br /> - 使用句子大小写<br />- 始终使用 Semilight 权重<br /><br /> **不要：**<br /><br /> - 粗体、italic 或粗体<br />- 用于正文文本<br />- 在工具窗口中使用|**显示为：18** pt Segoe UI Semillight<br /><br /> **视觉对象示例：**<br /><br /> ![Semilight 200% 环境字体&#43;示例](../../extensibility/ux-guidelines/media/0202-b_ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>155% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> - 文档井 UI 中的节标题<br />- 报表<br /><br /> **执行：** 使用句子大小写<br /><br /> **不要：**<br /><br /> - 粗体、italic 或粗体<br />- 用于正文文本<br />- 在标准控件Visual Studio使用<br />- 在工具窗口中使用|**显示为：14** pt Segoe UI<br /><br /> **视觉对象示例：**<br /><br /> ![155% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-c_ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>133% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> - 签名对话框中较小的子标题<br />- 文档井 UI 中的较小子标题<br /><br /> **执行：** 使用句子大小写<br /><br /> **不要：**<br /><br /> - 粗体、italic 或粗体<br />- 用于正文文本<br />- 在标准控件Visual Studio使用<br />- 在工具窗口中使用|**显示为：12** pt Segoe UI<br /><br /> **视觉对象示例：**<br /><br /> ![133% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-d_ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>122% 环境字体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中的节标题<br />-树视图中的顶级节点<br />-垂直选项卡导航<br /><br /> **Do：** 使用句子 case<br /><br /> **不要：**<br /><br /> -粗体、斜体或粗体斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 11 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![122% 环境字体标题的示例](../../extensibility/ux-guidelines/media/0202-e_ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>环境字体 + 粗体

|使用情况|外观|
|-|-|
|**用法：**<br /><br /> -签名对话框中的标签和副标题<br />-报表中的标签和副标题<br />-文档好 UI 中的标签和副标题<br /><br /> **看**<br /><br /> -Use 句型 case<br />-使用粗体<br /><br /> **不要：**<br /><br /> -斜体或斜体<br />-用于正文文本<br />-用于标准 Visual Studio 控件<br />-在工具窗口中使用|**显示为：** 加粗 9 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![环境字体 &#43; 粗体标题的示例](../../extensibility/ux-guidelines/media/0202-f_efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>环境字体

|使用情况|外观|
|-|-|
|**用法：** 所有其他文本<br /><br /> **Do：** 使用句子 case<br /><br /> **请勿：** 斜体或斜体|**显示为：** 9 pt Segoe UI<br /><br /> **Visual 示例：**<br /><br /> ![环境字体的示例](../../extensibility/ux-guidelines/media/0202-g_ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>填充和间距
 标题需要围绕它们的空间来为他们指定适当的强调。 此空间因点大小而异，其他在标题附近，例如水平标尺或环境字体中的文本行。

- 标题的理想填充方式应为大写字符高度空间的90%。 例如，一个 28 pt Segoe UI 光源标题的高度为26磅，并且填充长度应约为23磅，或者约31像素。

- 标题周围的最小空间应为大写字符高度的50%。 当标题附带一个规则或其他严格的元素时，可以使用较少的空间。

- 粗体环境字体文本应遵循默认行高度间距和填充。

## <a name="see-also"></a>另请参阅

- [字体 (Windows) ](/windows/desktop/uxguide/vis-fonts)
- [Windows) 的用户界面文本 (](/windows/desktop/uxguide/text-ui)
