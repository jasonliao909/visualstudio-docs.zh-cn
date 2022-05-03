---
title: 代码格式设置
description: 本文介绍可用于修改Visual Studio for Mac中的文本编辑器行为的各种选项
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 03/03/2022
ms.custom: devdivchpfy22
ms.topic: reference
ms.assetid: 81EE4460-26EB-4BB0-9297-932E1F88E4B8
ms.openlocfilehash: 633608013460f0a550b9807d953de49be3e1c53d
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144513587"
---
# <a name="editor-behavior"></a>编辑器行为

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

可以将编辑器行为设置为允许编写代码时进行格式设置。 可在“Visual Studio”>“首选项”>“文本编辑器”>“行为”下设置这些操作，以下介绍了一些常用的功能：

![编辑器行为选项](media/source-editor-image9.png)

* 创建新的类、方法或属性时，会自动将匹配的右大括号添加到代码。 选中此选项时，键入 `{` 将自动添加 `}`。
* 按下分号或大括号等字符会触发即时生成的代码格式，模拟已设置的格式首选项。
* 还可以选择在保存文件时格式化文件。 它允许根据需要编写代码，并使 IDE 负责按现有首选项设置代码的格式。
* 缩进可以设置为以下值：
  * 无 - 将脱字号设置到下一行的起始位置
  * 自动 - 将脱字号设置到下一行的同一列
  * 智能 - 基于代码在下一行缩进
* 断字行为在操作系统之间有所不同，出于导航目的，文本编辑器需要知道单词的开始或结束位置。 可以将格式设置为 Unix 或 Windows。

也可以为 XML、CSS、HTML 和 JSON 设置格式规则。

## <a name="see-also"></a>另请参阅

- [代码样式首选项（Windows 上的 Visual Studio）](/visualstudio/ide/code-styles-and-quick-actions)
