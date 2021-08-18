---
title: 代码段选择器
description: 了解如何使用代码片段选择器将现成的代码块插入到活动文档中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.expansionpicker
helpviewer_keywords:
- Code Snippet Picker
- IntelliSense code snippets, Code Snippet Picker
- code snippets, Code Snippet Picker
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 3ea8ffeb61cd83377e18d2e59a45ed1aa5d57d0e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122144114"
---
# <a name="code-snippet-picker"></a>代码段选择器

Visual Studio 代码编辑器提供一种代码片段选择器，让你单击几下鼠标即可将现成的代码块插入到活动文档中。

显示“代码片段选择器”的过程根据用户所使用的语言会有所不同。

- Visual Basic - 在代码编辑器中右键单击所需位置，显示快捷菜单，然后选择“插入代码段”。

- C# - 在代码编辑器中右键单击所需位置，显示快捷菜单，然后单击“插入代码段”或“外侧代码”。

- C++ - 代码片段选择器不可用。

- F# - 代码片段选择器不可用。

- JavaScript - 在代码编辑器中右键单击所需位置，显示快捷菜单，然后单击“插入代码段”或“外侧代码”。

- XML：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- HTML：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”或“外侧代码”。

- SQL：在代码编辑器中所需的位置处右击，以显示快捷菜单，然后单击“插入片段”。

在大多数 Visual Studio 开发语言中，可使用“代码片段管理器”将文件夹添加到文件夹列表，代码片段选择器会在该列表中扫描 XML 片段文件。 也可以创建自己的片段添加到该列表。 有关详细信息，请参见[演练：创建代码片段](../../ide/walkthrough-creating-a-code-snippet.md)。

## <a name="uielement-list"></a>UIElement 列表

项名称

可编辑文本字段，显示在“项列表”中选定的项的名称。 若要执行渐进式搜索以查找所需的项，请首先在此字段中键入其名称。 继续添加字母，直到在“项列表”中选定所需的项。

项列表

可以插入的代码片段的列表，或包含代码片段的文件夹的列表。 若要插入片段或展开文件夹，请选择所需的项，然后按 Enter。

## <a name="see-also"></a>请参阅

- [有关使用代码片段的最佳做法](../../ide/best-practices-for-using-code-snippets.md)
- [Visual Basic IntelliSense 代码段](/dotnet/visual-basic/developing-apps/using-ide/intellisense-code-snippets)
- [在代码中设置书签](../../ide/setting-bookmarks-in-code.md)
- [如何：使用外侧代码片段](../../ide/how-to-use-surround-with-code-snippets.md)
