---
title: 选项，文本编辑器，高级
description: 了解如何使用“高级”对话框更改 Visual Studio 文本编辑器的全局设置。
ms.date: 03/29/2022
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.Advanced
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: f0e9aaeb780ad2d52e3a21542c485534a87b8969
ms.sourcegitcommit: 864b18011ff12d880584173c86dccfdcc425808f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2022
ms.locfileid: "141347748"
---
# <a name="options-dialog-box-text-editor--advanced"></a>“选项”对话框：“文本编辑器”\>“高级”

可使用“高级”对话框更改 Visual Studio 代码和文本编辑器的全局设置。 若要显示该对话框，请从菜单栏中选择“工具”，然后选择“选项” > “文本编辑器” > “高级”。   

::: moniker range="vs-2022"

:::image type="content" source="media/vs-2022/tools-options-text-editor-advanced.png" alt-text="“选项”对话框中文本编辑器的高级设置的屏幕截图。":::

::: moniker-end

::: moniker range="vs-2019"

:::image type="content" source="media/vs-2019/tools-options-text-editor-advanced.png" alt-text="“选项”对话框中文本编辑器高级设置的屏幕截图。":::

::: moniker-end

## <a name="difference-display-mode"></a>差异显示模式

默认选中“整行”选项。 通过可供选择的选项，可在添加、删除或修改文本行时，自定义在差异查看器中显示的高亮内容和大纲内容。 具体而言，这些选项提供以下查看体验：

- **整行**：应显示行差异，使其填满整个视区宽度。
- **代码计数**：行差异只应显示到每行的最后一个字符。
- **块轮廓**：行差异和单词差异显示为空心矩形。
- **混合轮廓**：行差异显示为空心矩形，单词差异显示为彩色矩形。

## <a name="show-the-difference-overview-margin"></a>显示差异概述边距

此选项默认选中，它会在滚动条旁边添加一个边距视图来显示 Git 提交之间的差异。 红色表示删除，绿色表示添加。

## <a name="responsive-code-completion"></a>响应代码完成情况

默认选中，切换到关闭自动完成模式。

## <a name="word-based-suggestions-in-files-handled-by-textmate-grammars"></a>由 TextMate 语法处理的文件中基于单词的建议

Visual Studio 使用 [TextMate 语法](https://macromates.com/manual/en/language_grammars)在编辑器中提供备用编程语言支持和着色。 启用后，Visual Studio 自动完成功能将基于键入的单词而不是代码。 切换以关闭。

> [!TIP]
> 有关 TextMate 语法的详细信息，请参阅[添加对其他语言的 Visual Studio 编辑器支持](../adding-visual-studio-editor-support-for-other-languages.md)。

## <a name="default-intellisense-completion-mode"></a>默认 IntelliSense 完成模式

从以下完成模式设置中选择一个：

- 自动（默认设置），它会补全标点和特殊字符。
- 仅限 Tab，它仅补全 Tab。
- 上次使用的内容，它会保留上次通过 Ctrl+Alt+空格使用的设置。   

## <a name="allow-codelens-to-displace-the-caret-line"></a>允许 CodeLens 替换脱字号行

默认情况下，[CodeLens](../find-code-changes-and-other-history-with-codelens.md) 信息显示在代码行上方。 切换以改为直接在当前脱字号位置的代码行中显示 CodeLens 信息。

::: moniker range="vs-2022"

## <a name="use-box-selection"></a>使用框选择

此选项默认处于未选中状态，它提供用于 Visual Studio 2022 中新增的下列[多脱字号选择](../finding-and-replacing-text.md?view=vs-2022&preserve-view=true#multi-caret-selection)：

- 与 [VS Code](https://code.visualstudio.com/docs/editor/codebasics#_multiple-selections-multicursor) 中的多脱字号功能类似地采用“块选择”。
- 支持使用每个脱字号复制粘贴文本的不同部分，而不是仅限文本的单个块形状的部分。
- 按下箭头键时移动每个脱字号，并且不关闭块选择。

> [!NOTE]
> 选中后，此选项将应用 Visual Studio 2019 及更低版本中提供的框选择行为。 具体来说，借助此选项，在按下 Alt，然后拖动鼠标选择文本（或者按 Shift+Alt+Left/Up/Right/Down 来选择文本）时，可选择项的矩形部分。       此选项的局限在于，在按下箭头键时，Visual Studio 会关闭框选择并返回到单个脱字号。

## <a name="use-adaptive-formatting"></a>使用自适应格式

根据最新更新的文件，Visual Studio 会识别你是偏爱使用 Tab 还是空格来缩进代码。 自适应格式选项默认选中。 如果未选中，Visual Studio 转而使用“工具” > “选项” > “文本编辑器” > “所有语言” > “[选项卡](options-text-editor-all-languages-tabs.md)”中的设置。    

::: moniker-end

## <a name="copy-rich-text-on-copycut"></a>在复制/剪切时复制格式文本

此选项默认选中，它会复制包含颜色和连字的文本。 切换可改为复制平面文本。

> [!TIP]
> 如果取消选择此选项，会提高 Visual Studio 在复制/粘贴操作期间的响应能力和性能。 格式文本复制可能会导致 UI 延迟和临时挂起。

### <a name="max-length"></a>最大长度

使用此选项可增加或减少从代码复制或剪切的最大字符计数。 默认值设为 10240。

### <a name="use-accurate-classification"></a>使用准确分类

切换此复选框以允许语义着色。 几秒钟后可能会出现“等待”对话框。 （存在语法着色和语义着色，前者复制速度快，后者复制速度较慢。 语义信息允许更丰富、更准确的着色。）

## <a name="auto-cancel-long-running-auxiliary-operations-on-typing"></a>键入时自动取消长时间运行的辅助操作

此选项默认选中；通过它，在文本编辑器中键入内容时，Visual Studio 可停止后台任务。 换句话说，它控制 Visual Studio 如何严格取消在你键入内容时可能会暂时冻结 UI 的工作。

### <a name="automatically-adjust-maximum-allowed-typing-latency"></a>自动调整允许的最大键入延迟

此选项默认选中，它会调整在 Visual Studio 取消之前，功能或扩展可能导致键入操作的最大键入延迟。

### <a name="maximum-allowed-typing-latency-in-milliseconds"></a>允许的最大键入延迟（毫秒）

如果希望设置在文本编辑器中键入内容时 Visual Studio 应用的最大延迟，请选择此选项。

::: moniker range="vs-2019"

## <a name="use-adaptive-formatting"></a>使用自适应格式

根据最新更新的文件，Visual Studio 会识别你是偏爱使用 Tab 还是空格来缩进代码。 自适应格式选项默认选中。 如果未选中，Visual Studio 转而使用“工具” > “选项” > “文本编辑器” > “所有语言” > “[选项卡](options-text-editor-all-languages-tabs.md)”中的设置。    

::: moniker-end

## <a name="scrolling-sensitivity"></a>滚动敏感性

使用此选项可提高 Visual Studio 中的滚动性能。

### <a name="vertical-scrolling-sensitivity-lines-per-scroll"></a>垂直滚动敏感性（每次滚动的行数）

使用此选项可调整要在每个用户界面操作中滚动的垂直行数。 默认值设为 3。

### <a name="horizontal-scrolling-sensitivity-characters-per-scroll"></a>水平滚动敏感性（每次滚动字节数）

使用此选项可调整每个用户界面操作中要滚动的字符数。 默认值设为 1。

## <a name="text-formatting-method"></a>文本格式设置方法

默认为“自动”。 可选择另外两个选项之一：“理想”或“显示”。  根据特定硬件，选择最能让你在编辑器中微调文本格式的选项。

有关详细信息，请参阅 [TextFormattingMode](/dotnet/api/system.windows.media.textformattingmode?view=windowsdesktop-6.0&preserve-view=true)。

## <a name="text-rendering-method"></a>文本呈现方法

默认为“自动”。 可选择另外三个选项之一：ClearType“灰度”或“锯齿”。   根据特定硬件，选择最能让你在编辑器中微调文本呈现的选项。

有关更多信息，请参阅 [TextRenderingMode](/dotnet/api/system.windows.media.textrenderingmode?view=windowsdesktop-6.0&preserve-view=true)。

## <a name="see-also"></a>请参阅

[“选项”对话框：“文本编辑器”>“常规”](options-text-editor-general.md)