---
title: 在工作流中设置断点
description: 了解如何使用工作流设计器在图形工作流上设置断点，就像在 Visual Basic 或 C# 代码中设置断点一样。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e41b21c9-c061-4358-8e2f-eb5e412864a8
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- multiple
ms.openlocfilehash: 5a40b357c71fffd1ef44be4e904cd52b583fb956
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664680"
---
# <a name="how-to-set-breakpoints-in-workflows"></a>如何：在工作流中设置断点

使用工作流设计器时，可以在图形工作流上设置断点，就像在 Visual Basic 或 C# 代码中设置断点一样。 正如所料，工作流执行将在设置的每个断点处停止。

断点具有三个状态：“挂起”、“绑定”和“错误”。 当您设置断点时，断点处于“挂起”状态，并且由一个实心的红色图标表示。 当运行时加载了工作流类型后，断点将成为“绑定”状态。 如果为断点指定了不正确的格式（例如无效的活动名称），则会显示一个错误窗口。 断点仍然会添加到断点窗口，但标有一个小“x”。

> [!NOTE]
> 不支持在调用的工作流上设置断点。

> [!NOTE]
> 确保在调试之前，已从“工具” > “选项” > “调试”菜单中选择选项“启用‘仅我的代码’(仅限托管)”。 如果未选择此选项且在另一个序列中嵌套有两个序列，并且在第一个内部序列上设置一个断点，则按 F11 不会调试到第二个内部序列。

> [!NOTE]
> 如果 XAML 文件属性的完整路径不准确，则工作流中的断点不会命中。 将项目或解决方案移动到另一个文件夹或另一台计算机后，XAML 文件的完整路径不准确。 选择 Ctrl+S 以保存和更新完整路径属性。

## <a name="to-set-a-breakpoint-on-an-activity-in-the-design-view"></a>在设计视图中的活动上设置断点

1. 选择希望调试器在其上中断的活动。

2. 在“调试”菜单上，选择“切换断点”。 此时将在该活动的左上边缘显示一个红色图标。

   此外，还可以在选择该活动后按 F9，或者右键单击该活动，然后从右键菜单中选择“断点” > “插入断点”。

## <a name="see-also"></a>另请参阅

- [使用工作流设计器调试工作流](../workflow-designer/debugging-workflows-with-the-workflow-designer.md)
- [如何：使用工作流设计器调试 XAML](../workflow-designer/how-to-debug-xaml-with-the-workflow-designer.md)
