---
title: 预览代码更改
description: 了解如何在接受即将对项目所做的修改前通过“预览更改”窗口浏览这些内容。
ms.custom: SEO-VS-2020
ms.date: 12/16/2016
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
f1_keywords:
- vs.codefix.previewchanges
ms.workload:
- multiple
ms.openlocfilehash: 463778da41f7091981434203900f078efe848a2d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641598"
---
# <a name="preview-changes-window"></a>预览更改窗口

在 Visual Studio 中使用各种 *快速操作* 或 *重构* 工具时，在接受更改之前通常可以预览要对项目所做的更改。 可以在“预览更改”窗口中完成此操作。  例如，下面的 **预览更改** 窗口显示在 C# 项目中重命名重构过程中的更改内容：

![预览更改](media/previewchanges.png)

窗口的上半部分显示要更改的特定行，每个行都有一个复选框。 如果想要有选择地将重构应用于特定行，可以选中或取消选中各个复选框。

窗口的下半部分显示项目中要更改的格式化代码，并且突出显示受影响的区域。 在窗口的上半部分中选择特定的行将突出显示窗口下半部分的相应行。 这样，可以快速跳到相应的行并查看周围的代码。

检查所做的更改之后，单击“应用”按钮以提交这些更改，或单击“取消”按钮保持内容不变。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中重构](../ide/refactoring-in-visual-studio.md)
- [快速操作](../ide/quick-actions.md)
