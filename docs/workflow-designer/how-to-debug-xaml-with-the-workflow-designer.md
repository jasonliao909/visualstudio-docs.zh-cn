---
title: 工作流设计器：调试 XAML
description: 了解如何根据 XAML 定义工作流，以及如何使用应用程序调试 XAML 工作流设计器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d9305dbc-af62-4bdd-b03f-c54e3fe9ecc7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- uwp
ms.openlocfilehash: 721ee723c6f7d0e28c4d7da376233641a580d21d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602186"
---
# <a name="how-to-debug-xaml-with-the-workflow-designer"></a>如何：使用工作流设计器调试 XAML

工作流是以 XAML 的形式定义的。 工作流的 UI 表示形式建立在定义该工作流的 XAML 树之上。 调试体验类似于调试工作流中的工作流设计器。 例如，调试 XAML 时，局部点、监视和线程窗口的工作方式与调试工作流设计器相同。 此外，在 XAML 调试过程中，“调用堆栈”视图是工作流执行流的基于行的分层视图。

> [!NOTE]
> 如果工作流的 XAML 位于活动所在的同一程序集中，将不包括类名称的程序集部分。 如果没有类的此部分 (活动) 名称，则不能运行时加载 XAML。 建议不要在主项目所在的同一命名空间中定义活动；否则，在设计器中编辑后需要手动编辑 XAML。

## <a name="to-debug-workflow-xaml"></a>调试工作流 XAML

1. 在 Visual Studio 中打开工作流或Visual Studio。

2. 在要调试的活动上设置断点，如如何：在工作流 中设置 [断点中所述](../workflow-designer/how-to-set-breakpoints-in-workflows.md)。

3. 右键单击包含工作流定义的 .xaml 文件，然后选择"**查看代码"。** 您将看到在设计视图中对其设置了断点的活动的 XAML 元素声明所在行中显示了一个断点。

4. 调用调试器，如调试 [工作流 中所述](debugging-workflows-with-the-workflow-designer.md)。

5. 当代码执行到你设置的其中一个断点处时，与该断点关联的 XAML 元素将突出显示。 若要移动到下一个断点，请使用 **F10** 或 **F11** 键。

## <a name="see-also"></a>另请参阅

- [如何：在工作流中设置断点](../workflow-designer/how-to-set-breakpoints-in-workflows.md)
- [调试工作流](debugging-workflows-with-the-workflow-designer.md)
