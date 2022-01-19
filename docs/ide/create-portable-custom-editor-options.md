---
title: EditorConfig 设置
description: 了解如何向项目或代码库添加 EditorConfig 文件，强制对使用该代码库的所有人实施一致的编码样式。
ms.custom: SEO-VS-2020, devdivchpfy22
ms.date: 01/07/2021
ms.topic: how-to
helpviewer_keywords:
- editorconfig [Visual Studio]
author: mikadumont
ms.author: midumont
manager: jmartens
ms.technology: vs-ide-general
ms.openlocfilehash: 67bd6e342bf65b40e07a0b6f0e5fb9fc5b9c97e6
ms.sourcegitcommit: 658edd3b0dc23fb20728dafc12734b22f8ed1a89
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2022
ms.locfileid: "136890703"
---
# <a name="create-portable-custom-editor-settings-with-editorconfig"></a>使用 EditorConfig 创建可移植的自定义编辑器设置

可以向项目或基本代码添加 EditorConfig 文件，强制对使用该基本代码的所有人实施一致的编码样式。 EditorConfig 设置优先于全局 Visual Studio 文本编辑器设置。 这意味着，可以调整每种基本代码，以使用特定于该项目的文本编辑器设置。 仍然可以在 Visual Studio“选项”对话框中设置个人编辑器首选项。 以下两种情况下将应用这些设置：每当在不具备 .editorconfig 文件的代码库中执行操作时，或者当 .editorconfig 文件不会替代特定设置时 。 此类首选项的一个示例为缩进样式 &mdash; 制表符或空格。

许多代码编辑器和 Ide （包括 Visual Studio）都支持 EditorConfig 设置。 它是一种随代码移动的可移植组件，甚至可以在 Visual Studio 外强制实施编码样式。

::: moniker range=">=vs-2019"

将 EditorConfig 文件添加到 Visual Studio 中的项目时，会根据 EditorConfig 设置设置新的代码行的格式。 除非你运行以下命令之一，否则不会更改现有代码的格式：

 - [代码清除](../ide/code-styles-and-code-cleanup.md) (**ctrl** + **K**， **ctrl** + **E**) ，它应用任何空白设置，如缩进样式和所选的代码样式设置，如如何对指令进行排序 `using` 。
 - **编辑** >**高级** >在默认配置文件) 中设置 **文档格式** (或 **ctrl** + **K**， **ctrl** + **D** ，只应用空白设置，如缩进样式。

 ::: moniker-end

::: moniker range="=vs-2017"

将 EditorConfig 文件添加到 Visual Studio 中的项目时，会根据 EditorConfig 设置设置新的代码行的格式。 除非在  >  默认配置文件) 中设置文档格式 (编辑高级  >  **格式文档** 或按 ctrl  + **K**， **ctrl** + **D** ，否则不会更改现有代码的格式。 设置文档格式只会影响空格设置，如缩进样式，除非已配置格式文档来 [执行其他代码清除](../ide/code-styles-and-code-cleanup.md#apply-code-styles)。

 ::: moniker-end

::: moniker range="vs-2017"

可定义希望“设置文档格式”在[“设置格式”选项](reference/options-text-editor-csharp-formatting.md#format-document-settings)页面上应用的 EditorConfig 设置 。

::: moniker-end

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[Visual Studio for Mac 中的 EditorConfig](/visualstudio/mac/editorconfig)。

## <a name="code-consistency"></a>代码一致性

EditorConfig 文件中的设置使你可以在基本代码中保持一致的编码风格和设置，例如缩进样式、选项卡宽度、行尾字符、编码等，而不考虑使用的编辑器或 IDE。 例如，使用 C# 编码时，如果基本代码约定为始终缩进五个空格字符、文档使用 UTF-8 编码，且每一行始终以 CR/LF 结束，则可以配置 .editorconfig 文件达到此效果。

您在个人项目中使用的编码约定可能不同于团队项目中使用的编码约定。 例如，你可能倾向在编码时，缩进操作会添加制表符。 但你的团队可能更倾向使用四个空格字符的缩进，而不是制表符。 EditorConfig files 通过允许每个方案都有一个配置来解决此问题。

由于基本代码中的文件包含这些设置，因此它们与该基本代码一起传送。 只要在 EditorConfig 兼容的编辑器中打开代码文件，就会激活文本编辑器设置。 有关 EditorConfig 文件的详细信息，请参阅 [EditorConfig.org](https://editorconfig.org/) 网站。

> [!NOTE]
> 在 EditorConfig 文件中设置的约定当前无法在 CI/CD 管道中强制为生成错误或警告。 任何样式偏差都仅显示在 Visual Studio 编辑器和“错误列表”中。

## <a name="supported-settings"></a>支持的设置

Visual Studio 中的编辑器支持 [EditorConfig 属性](https://editorconfig.org/#supported-properties)的核心集：

- indent_style
- indent_size
- tab_width
- end\_of_line
- charset
- trim\_trailing_whitespace
- insert\_final_newline
- 根

除 XML 支持 EditorConfig 编辑器设置外，所有 Visual Studio 支持的语言。 此外，EditorConfig 还支持[代码样式](/dotnet/fundamentals/code-analysis/code-style-rule-options)约定，包括 c # 和 Visual Basic 的[语言](/dotnet/fundamentals/code-analysis/style-rules/language-rules)、[格式](/dotnet/fundamentals/code-analysis/style-rules/formatting-rules)和[命名](/dotnet/fundamentals/code-analysis/style-rules/naming-rules)约定。

## <a name="add-and-remove-editorconfig-files"></a>添加和删除 EditorConfig 文件

向项目或基本代码添加 EditorConfig 文件后，将按照 EditorConfig 文件设置编写的所有新代码行的格式。 然而，添加 EditorConfig 文件并不会将现有样式转换为新样式，直到您设置文档格式或运行 [代码清除](../ide/code-styles-and-code-cleanup.md)为止。 例如，如果文件中的缩进格式设置了选项卡，并且添加了使用空格缩进的 EditorConfig 文件，则缩进字符不会自动转换为空格。 如果对文档进行格式设置 (**编辑**  >  **高级**  >  **格式文档** 或 **ctrl** + **K**、 **ctrl** + **D**) ，则 EditorConfig 文件中的空白设置将应用于现有的代码行。

如果从项目或基本代码库中删除 EditorConfig 文件，并想要使用全局编辑器设置设置新代码行的格式，必须关闭并重新打开任何打开的代码文件。

### <a name="add-an-editorconfig-file-to-a-project"></a>将 EditorConfig 文件添加到项目

1. 在 Visual Studio 中打开项目或解决方案。 根据要应用 .editorconfig 设置的对象（是解决方案中的所有项目还是其中一个项目），选择项目或解决方案节点。 还可在项目或解决方案中选择一个文件夹，向其添加 .editorconfig 文件。

1. 从菜单栏中，选择“项目” > “添加新项”，或按 Ctrl+Shift+A    。

   此时将打开“添加新项”对话框。

1. 在搜索框中，搜索“editorconfig”。

   搜索结果将显示两个 editorconfig 文件项模板。

   ![Visual Studio 中的 EditorConfig 文件项模板](media/vs-2022/editorconfig-item-templates-new.png)

1. 选择“editorconfig 文件(默认)”模板，添加使用针对缩进样式和尺寸的两个核心 EditorConfig 选项预填充的 EditorConfig 文件。 或者，选择“editorconfig 文件(.NET)”模板，添加使用默认的 [.NET 代码样式、格式设置和命名约定](/dotnet/fundamentals/code-analysis/code-style-rule-options)预填充的 EditorConfig 文件。

   解决方案资源管理器中随即显示一个 .editorconfig 文件，且文件在编辑器中打开。

   ![解决方案资源管理器和编辑器中的 .editorconfig 文件](media/vs-2022/editorconfig-dotnet-new.png)

1. 根据需要编辑文件。

### <a name="other-ways-to-add-an-editorconfig-file"></a>添加 EditorConfig 文件的其他方式

可以通过以下几种方法将 EditorConfig 文件添加到项目中：

- 用于 Visual Studio 的 IntelliCode 的[代码推断功能](/visualstudio/intellicode/code-style-inference)通过现有代码推断代码样式。 然后它将使用已定义的代码样式首选项创建非空的 EditorConfig 文件。

- 自 Visual Studio 2019 起，可以通过“工具” > “选项”[基于代码样式设置生成 EditorConfig 文件](code-styles-and-code-cleanup.md#code-styles-in-editorconfig-files)。 

## <a name="file-hierarchy-and-precedence"></a>文件层次结构和优先级

如果将 .editorconfig 文件添加到文件层次结构中的某文件夹，则其设置将应用于该级别及更低级别的所有适用文件。 还可替代特定项目、代码库或部分代码库的 EditorConfig 设置，以使其使用与代码库其他部分不同的约定。 当要包含其他地方的代码而不想更改其约定时，这会很有用。

若要替代部分或全部 EditorConfig 设置，请在要应用这些替代设置的文件层次结构级别添加 .editorconfig 文件。 新的 EditorConfig 文件设置应用于同级目录和任何子目录中的文件。

![EditorConfig 层次结构](../ide/media/vside_editorconfig_hierarchy.png)

如果想替代一部分而非所有设置，请在 .editorconfig 文件中仅指定这些设置。 仅替代较低级别文件中显式列出的属性。 更高级别 .editorconfig 文件中的其他设置会继续应用。

如果要确保 _任何_ 更高级别的 .editorconfig 文件中 _没有_ 设置应用于此部分代码库，请将 ```root=true``` 属性添加到较低级别的 .editorconfig 文件中 ：

```ini
# top-most EditorConfig file
root = true
```

从上到下读取 EditorConfig 文件。 如果有多个具有相同名称的属性，则最近找到的具有该名称的属性具有优先权。

## <a name="edit-editorconfig-files"></a>编辑 EditorConfig 文件

Visual Studio 提供 IntelliSense 完成列表，帮助你编辑 .editorconfig 文件。

![.editorconfig 文件中的 IntelliSense](media/vs-2022/editorconfig-intellisense-no-extension-new.png)

编辑 EditorConfig 文件后，必须重载代码文件，新设置才会生效。

如果编辑多个 *editorconfig* 文件，则可能会发现 [editorconfig 语言服务扩展](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) 很有用。 该扩展的一些功能包括语法高亮显示、改进的 IntelliSense、验证和代码格式。

![带有 EditorConfig 语言服务扩展的 IntelliSense](media/editorconfig-intellisense.png)

## <a name="example"></a>示例

以下示例演示将 .editorconfig 文件添加到项目之前和之后 C# 代码片段的缩进状态。 Visual Studio 文本编辑器“选项”对话框中的“Tab”设置设置为按 Tab 键时可生成空格字符。  

![文本编辑器 Tab 设置](../ide/media/vs-2022/vside_editorconfig_tabsetting-new.png)

按预期，在下一行按 **tab** 键将增加四个空白字符，从而缩进该行。

![使用 EditorConfig 之前的代码](../ide/media/vs-2022/vside_editorconfig_before-new.png)

将具有以下内容的名为 .editorconfig 的新文件添加到项目。 `[*.cs]` 设置意味着此更改仅应用于项目中的 C# 代码文件。

```ini
# Top-most EditorConfig file
root = true

# Tab indentation
[*.cs]
indent_style = tab
```

现在按 **Tab** 键时，会获得制表符而不是空格。

![使用 Tab 键添加制表符](../ide/media/vside_editorconfig_tab.png)

## <a name="troubleshoot-editorconfig-settings"></a>EditorConfig 设置疑难解答

如果在目录结构中处于或高于你项目所在位置的任何位置存在 EditorConfig 文件，则 Visual Studio 会将该文件中的编辑器设置应用于编辑器。 在这种情况下，你可能会在状态栏中看到以下消息：

   “该项目编码约定覆盖了此文件类型的用户首选项”。

这意味着如果目录结构中与项目位于相同位置或在项目之上的某个 EditorConfig 文件中指定了“工具” > “选项” > “文本编辑器”中的任何编辑器设置（如缩进尺寸和样式、制表符大小或编码约定），则 EditorConfig 文件中的约定会替代“选项”中的设置   。 可以通过在“工具” > “选项” > “文本编辑器”中切换“遵循项目编码约定”选项来控制此行为。 取消选中该选项会关闭 Visual Studio 的 EditorConfig 支持。

![工具选项 - 遵循项目编码约定](media/vs-2022/coding_conventions_option-new.png)

还可以通过打开命令提示符并从包含项目的磁盘的根目录运行以下命令，在父目录中查找任何 .editorconfig 文件：

```Shell
dir .editorconfig /s
```

可以通过在存储库的根目录或项目所在目录的 .editorconfig 文件中设置 ```root=true``` 属性，控制 EditorConfig 约定的范围。 Visual Studio 会在打开的文件的目录和每个父目录中查找名为 .editorconfig 的文件。 到达根文件路径时或找到具有 ```root=true``` 的 .editorconfig 文件时搜索结束。

## <a name="see-also"></a>请参阅

- [.NET 代码样式约定](/dotnet/fundamentals/code-analysis/code-style-rule-options)
- [支持语言服务的 EditorConfig](../extensibility/supporting-editorconfig.md)
- [EditorConfig.org](https://editorconfig.org/)
- [代码编辑器功能](writing-code-in-the-code-and-text-editor.md)
- [EditorConfig (Visual Studio for Mac)](/visualstudio/mac/editorconfig)
