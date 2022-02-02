---
title: 查找和替换文本以及多个插入点选择
description: 了解“查找和替换”功能，并了解如何使用它查找和替换模式的实例。
ms.custom: SEO-VS-2020
ms.date: 02/01/2022
ms.topic: conceptual
f1_keywords:
- vs.find
- vs.findreplacecontrol
- vs.findreplace.findsymbol
- vs.findreplace.symbol
- findresultswindow
- vs.findreplace.quickreplace
- vs.findsymbol
- vs.findresults1
- vs,findsymbolwindow
- vs.findreplace.quickfind
- vs.lookin
- vs.replace
helpviewer_keywords:
- text searches
- Replace in Files dialog box
- Find in Files dialog box
- text searches, finding and replacing text
- text, finding and replacing
- find and replace
- find text
- replace text
- multi-caret selection
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 60a97bb589ce05ba95f1af4b2b92fc90dd1e9877
ms.sourcegitcommit: 3766c051f9a8b35106b16f751db7fecde0b92254
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "137951697"
---
# <a name="find-and-replace-text"></a>查找和替换文本

可以使用[查找和替换](#find-and-replace-control)（Ctrl+F 或 Ctrl+H）或[在文件中查找/替换](#find-in-files-and-replace-in-files)（Ctrl+Shift+F 或 Ctrl+Shift+H），在 Visual Studio 编辑器中查找和替换文本。 也可通过使用[多个插入点选择](#multi-caret-selection)来仅查找并替换模式的一些实例。

> [!TIP]
> 如果要重命名代码符号（例如变量和方法），最好 *[重构](../ide/reference/rename.md)* 它们，而不是使用查找和替换。 重构不仅智能而且知道应用范围，而查找和替换会盲目替换所有实例。

查找和替换功能在此编辑器中、其他某些基于文本的窗口（例如“查找结果”窗口）中、设计器窗口（如 XAML 设计器和 Windows 窗体设计器）中以及工具窗口中均提供。

可以将搜索范围限制到当前文档、当前解决方案或一组自定义文件夹中。 还可以指定一组文件扩展名，用于多文件搜索。 使用 .NET [正则表达式](../ide/using-regular-expressions-in-visual-studio.md)自定义搜索语法。

> [!TIP]
> [查找/命令](../ide/find-command-box.md)框可用作工具栏控件，但默认为不可见。 要显示“查找/命令”框，请在“标准”工具栏上选择“添加或删除按钮”，然后选择“查找”。

## <a name="find-and-replace-control"></a>“查找和替换”控件

- 按 Ctrl+F 作为查找当前文件中的字符串的快捷方式 。
- 按“Ctrl”+“H”作为快捷方式，以查找和替换当前文件中的字符串 。

“查找和替换”控件显示在代码编辑器窗口的右上角。 此操作会立即突出显示给定搜索字符串在当前文档中的每个匹配项。 通过在搜索控件上选择“查找下一个”按钮或“查找上一个”按钮，可以从一个匹配项导航到另一个匹配项。

::: moniker range="vs-2022"

:::image type="content" source="media/vs-2022/find-and-replace-box.png" alt-text="屏幕截图显示了 Visual Studio 2022 的编辑器中的“查找和替换”对话框。":::

::: moniker-end

::: moniker range="<=vs-2019"

:::image type="content" source="media/find-and-replace-box.png" alt-text="屏幕截图显示了 Visual Studio 2019 及较低版本的编辑器中的“查找和替换”对话框。":::

::: moniker-end

通过选择“查找”文本框旁边的按钮，可以访问替换选项。 若要一次替换一个，请选择“替换”文本框旁边的“替换下一个”按钮。 若要替换所有匹配项，请选择“全部替换”按钮。

若要更改匹配项的突出显示颜色，请依次选择“工具”菜单、“选项”、“环境”、“字体和颜色”。 在“显示设置对象”列表中，选择“文本编辑器”，然后在“显示项”列表中，选择“查找匹配突出显示项”   。

### <a name="search-tool-windows"></a>搜索工具窗口

通过选择“编辑” > “查找和替换”或按 Ctrl+F，可以在代码或文本窗口（如“输出”窗口和“查找结果”窗口）中使用“查找”控件。

某些工具窗口也提供某版本的“查找”控件。 例如，通过在搜索框中输入文本可以在“工具箱”窗口中筛选控件列表。 可以在其中搜索内容的其他工具窗口包括“解决方案资源管理器”、“属性”窗口和“团队资源管理器”。

## <a name="find-in-files-and-replace-in-files"></a>“在文件中查找”和“在文件中替换”

- 按 Ctrl+Shift+F 作为查找多个文件中的字符串的快捷方式  。
- 按 Ctrl+Shift+H 作为查找和替换多个文件中的字符串的快捷方式  。

“在文件中查找/替换”与“查找和替换”控件类似，区别在于可以定义搜索范围。 不仅可以搜索当前在编辑器中打开的文件，还可以搜索所有打开的文档、整个解决方案、当前项目，及所选文件夹集。 还可以按文件扩展名搜索。 要访问“在文件中查找/替换”对话框，请在“编辑”菜单上选择“查找和替换”（或按 Ctrl+Shift+F）     。

::: moniker range=">=vs-2022"

:::image type="content" source="media/vs-2022/find-files.png" alt-text="Visual Studio 2022 中“查找和替换”对话框的屏幕截图，其中打开了“在文件中查找”选项卡。":::

有关更多详细信息，请参阅 " [在文件中查找](find-in-files.md) " 和 " [在文件中替换](replace-in-files.md) " 页。

::: moniker-end

::: moniker range="vs-2019"

:::image type="content" source="media/find-files-vs2019.png" alt-text="Visual Studio 2019 中“查找和替换”对话框的屏幕截图，其中打开了“在文件中查找”选项卡。":::

有关更多详细信息，请参阅 " [在文件中查找](find-in-files.md) " 和 " [在文件中替换](replace-in-files.md) " 页。

> [!IMPORTANT]
> 如果使用 Visual Studio 2019 [版本 16.6](/visualstudio/releases/2019/release-notes-v16.6/) 或更早的版本，则“查找和替换”对话框可能与此处显示的不同。 切换到本页的 [Visual Studio 2017](?view=vs-2017&preserve-view=true) 版本，查看与屏幕上显示的内容相匹配的说明。

::: moniker-end

::: moniker range="vs-2017"

:::image type="content" source="media/find-files-vs2017.png" alt-text="Visual Studio 2017 中“查找和替换”对话框的屏幕截图，其中打开了“在文件中查找”选项卡。":::

有关更多详细信息，请参阅 " [在文件中查找](find-in-files.md) " 和 " [在文件中替换](replace-in-files.md) " 页。

::: moniker-end

### <a name="find-results"></a>查找结果

选择“查找全部”后，“查找结果”窗口随即打开，并列出搜索的匹配项。 在列表中选择一个结果会显示相关联的文件，并突出显示匹配项。 如果文件尚未打开进行编辑，则可以在选项卡右侧的预览选项卡中打开。 可以使用“查找”控件在“查找结果”列表中搜索。

### <a name="create-custom-search-folder-sets"></a>创建自定义搜索文件夹集

通过选择“查找范围”框旁边的“选择搜索文件夹”按钮（类似于...），可以定义搜索范围。 在“选择搜索文件夹”对话框中，可以指定要搜索的一组文件夹，并且可以保存规范，供以后重复使用。

> [!TIP]
> 如果已将远程计算机的驱动器映射到本地计算机，则可以指定要在远程计算机上搜索的文件夹。

### <a name="create-custom-component-sets"></a>创建自定义组件集

通过选择“查找范围”框旁边的“编辑自定义组件集”按钮，可以将组件集定义为搜索范围。 可以指定已安装的 .NET 或 COM 组件，以及包含在解决方案或任何程序集或类型库（.dll、.tlb、.olb、.exe 或 .ocx）中的 Visual Studio 项目。 若要搜索引用，请选择“查找引用”框。

## <a name="multi-caret-selection"></a>多个插入点选择

> [!NOTE]
> 本部分适用于 Windows 上的 Visual Studio。 对于 Visual Studio for Mac，请参阅[块选择](/visualstudio/mac/block-selection)。

::: moniker range="vs-2017"

**在 Visual Studio 2017 版本 15.8 中引入**

::: moniker-end

使用“多个插入点选择”同时在两个或多个位置进行相同编辑。 例如，可同时插入相同的文本或修改多个位置的现有文本。

::: moniker range="vs-2022"

在 Visual Studio 2022 中，改进了多插入点复制和粘贴体验。 以前，将多行粘贴到多个插入点时，会在每个插入点复制整个剪贴板。 现在，将多行粘贴到相同数量的插入点时，会将每一行插入相应的插入点。

若要使用多插入点，请按 Alt+Shift+鼠标单击，或按 Alt+Shift+.      然后，使用 Ctrl+Shift+箭头键来展开选择项  。 接下来，按 Ctrl+C 复制多个选择项中的文本 。 使用 Alt+Shift+鼠标单击，为每一行创建多个要粘贴到所需位置的插入点  。 最后，按 Ctrl+V 将每行粘贴到其自己的插入点 。

:::image type="content" source="media/vs-2022/multi-caret-copy-paste.gif" alt-text="Visual Studio 中多插入点选择操作的动画。":::

此外，可使用 Alt+Shift+向上键（或向下键），或者使用 Alt+Shift+鼠标拖动，来选择多个插入点      。 以前，这些笔势会创建框选择。 现在，框选择将转换为多个插入点。 与在精确位置单击以插入单独的插入点相比，此方法操作起来更容易且速度更快。

> [!TIP]
> 如果希望在展开多插入点选择时将框选择与 Alt+Shift+箭头键和 Alt+Shift+鼠标拖动一起使用，请转到“工具” > “选项” > “文本编辑器” > “高级”，然后选择“使用框选择”           。

### <a name="commands"></a>命令

以下键盘快捷键适用于特定于多插入点选择行为的操作。

|快捷方式|操作|命令|
|-|-|-|
| **Alt** +**移位** +**.** | 使用多插入符号 | 编辑.插入下一个匹配的 Caret |
| **Ctrl** +**移位** +**箭头键** | 展开选定内容 | 编辑. SizeControlUp、SizeControlDown、SizeControlRight、SizeControlLeft |
| **Alt** +**移位** +**向上** 键 (或 **向下** 键) | 选择多个插入符号 | 编辑. LineUpExtendColumn、LineDownExtendColumn |

你也可以通过选择“编辑”>“多个插入点”，然后选择所需的操作，从菜单栏中访问多插入点选择 。

:::image type="content" source="media/vs-2022/edit-menu-multiple-carets-find-replace.png" alt-text="Visual Studio 2022 中的“多个插入点”飞出式菜单的屏幕截图。":::

::: moniker-end

::: moniker range="<=vs-2019"

在以下屏幕截图中，在三个位置选择了 `-0000`；如果用户按 Delete，则删除所有三个选项：

![Visual Studio 中 XML 文件中的多个插入点选择](media/multi-caret-selection.png)

若要选择多个插入符号，请像往常一样单击或进行第一次文本选择，然后在单击或选择其他位置中的文本时按 **Ctrl** + **Alt** 。 还可自动添加匹配的文本作为其他选择，或选择一个文本框以在每行上进行相同的编辑。

> [!TIP]
> 如果已在 "**工具**  >  " "**选项**  >   >  " "常规" "**常规**" 中，选择 " **Alt** " 作为 "从 有关详细信息，请参阅选项 [对话框：文本编辑器 />常规](reference/options-text-editor-general.md)。

### <a name="commands"></a>命令

对多个插入点选择行为使用以下键和操作：

|快捷方式|操作|
|-|-|
|**Ctrl**+**Alt** + 单击|添加辅助插入点|
|**Ctrl**+**Alt** + 双击|添加辅助字选择|
|**Ctrl**+**Alt** + 单击 + 拖动|添加辅助选择|
|**Shift**+**Alt**+ **.**|添加下一个匹配文本作为选择|
|Shift+Alt+；|添加所有匹配的文本作为选择|
|**Shift**+**Alt**+ **,**|删除上次选择的匹配项|
|Shift+Alt+/|跳过下一个匹配的项|
|**Alt** + 单击|添加框选择|
|**Esc** 或单击|清除所有选择项|

“编辑”菜单上的“多个插入点”下也提供了一些命令：

:::image type="content" source="media/edit-menu-multiple-carets-find-replace.png" alt-text="Visual Studio 中的“多个插入点”飞出式菜单的屏幕截图":::

::: moniker-end

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中使用正则表达式](../ide/using-regular-expressions-in-visual-studio.md)
- [在 Visual Studio 中重构代码](../ide/refactoring-in-visual-studio.md)
- [块选择 (Visual Studio for Mac)](/visualstudio/mac/block-selection)
