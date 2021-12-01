---
title: 字符串可视化工具（文本、XML、HTML、JSON）
description: 在 Visual Studio 中进行调试时，使用内置字符串可视化工具对话框查看字符串。
ms.date: 10/10/2021
ms.custom: contperf-fy21q4
ms.topic: reference
f1_keywords:
- vs.debug.stringviewer
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
ms.assetid: 080fd8f1-72b0-461f-8451-3c84d5dc51df
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: da842df7f92bdcdbd5463755a9c56b5d42613778
ms.sourcegitcommit: 4efdab6a579b31927c42531bb3f7fdd92890e4ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2021
ms.locfileid: "130350802"
---
# <a name="view-text-xml-html-json-strings-in-the-string-visualizer"></a>在字符串可视化工具中查看文本、XML、HTML、JSON 字符串

在 Visual Studio 中进行调试时，可以使用内置字符串可视化工具查看字符串。 字符串可视化工具显示对于数据提示或调试器窗口而言过长的字符串。 它还可以帮助识别格式错误的字符串。

内置的字符串可视化工具包括[文本](#text-string-data)、[XML](#xml-string-data)、[HTML](#html-string-data) 和 [JSON](#json-string-data) 选项。 也可以从“自动”或其他调试器窗口中打开一些其他类型的内置可视化工具，例如 [DataSet、DataTable 和 DataView](../debugger/dataset-visualizer-dialog-box.md) 对象。

> [!NOTE]
> 如果需要在可视化工具中检查 XAML 或 WPF UI 元素，请参阅[在调试时检查 XAML 属性](../xaml-tools/inspect-xaml-properties-while-debugging.md)或[如何使用 WPF 树可视化工具](../debugger/how-to-use-the-wpf-tree-visualizer.md)。

## <a name="open-the-visualizer"></a>打开可视化工具

若要打开字符串可视化工具：
1. 调试期间暂停。 
2. 将鼠标悬停在具有纯文本、XML、HTML 或 JSON 字符串值的变量上。
3. 选择放大镜图标 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")。

## <a name="uielement-list"></a>UIElement 列表

“表达式”字段显示正将鼠标悬停在其上方的变量或表达式。

“值”字段显示字符串值。 空白值表示所选可视化工具无法识别该字符串。 例如，对于没有 XML 标记的文本字符串或 JSON 字符串，XML 可视化工具会显示空白值。 若要查看所选可视化工具无法识别的字符串，请改用文本可视化工具。 文本可视化工具可显示纯文本。

### <a name="text-string-data"></a>文本字符串数据

文本可视化工具可显示纯文本。 如果需要自定义 C++ 字符串的格式，请创建 [Natvis 可视化效果](../debugger/create-custom-views-of-native-objects.md)。

![文本字符串可视化工具](../debugger/media/dbg-string-visualizer-text.png "文本字符串可视化工具")

### <a name="json-string-data"></a>JSON 字符串数据

在 JSON 可视化工具中，格式正确的 JSON 字符串类似于下图。 格式错误的 JSON 可能会显示错误图标（如果无法识别，则为空白）。 若要标识 JSON 错误，请将字符串复制并粘贴到 JSON linting 工具，例如 [JSLint](https://www.jslint.com/)。

![JSON 字符串可视化工具](../debugger/media/dbg-tips-string-visualizer-json.png "JSON 字符串可视化工具")

### <a name="xml-string-data"></a>XML 字符串数据

在 XML 可视化工具中，格式正确的 XML 字符串类似于下图。 格式错误的 XML 可能在没有 XML 标记的情况下显示，如果无法识别则显示为空白。

![XML 字符串可视化工具](../debugger/media/dbg-string-visualizers-xml.png "XML 字符串可视化工具")

### <a name="html-string-data"></a>HTML 字符串数据

格式正确的 HTML 字符串的显示方式与在浏览器中的呈现方式相似，如下图所示。 格式错误的 HTML 可能显示为纯文本。

![HTML 字符串可视化工具](../debugger/media/dbg-string-visualizers-html.png "HTML 字符串可视化工具")

## <a name="see-also"></a>请参阅

- [创建自定义可视化工具（C#、Visual Basic）](../debugger/create-custom-visualizers-of-data.md)
- [Visual Studio for Mac 中的数据可视化效果](/visualstudio/mac/data-visualizations)
