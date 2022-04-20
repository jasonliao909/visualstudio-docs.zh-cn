---
title: 在表格可视化工具中查看 IEnumerable | Microsoft Docs
description: 使用 Visual Studio 调试器中的表可视化工具查看 IEnumerable。
ms.date: 04/08/2022
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
helpviewer_keywords:
- string visualizer
- visualizers, string
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
monikerRange: '>= vs-2022'
ms.workload:
- multiple
ms.openlocfilehash: 7fef0a09bec32fd421ae72b81f08685fd54451d2
ms.sourcegitcommit: 02b5dbdec3ae86c3dfb8c15344a2c195db7b424a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2022
ms.locfileid: "142649438"
---
# <a name="view-ienumerables-in-a-table-visualizer-in-visual-studio"></a>在 Visual Studio 的表格可视化工具中查看 IEnumerable

从 Visual Studio 2022 Update 2 预览版 1 开始，可在表格视图中查看 IEnumerable 集合。

IEnumerable 表可视化工具有助于以更简化的方式浏览大型集合对象。 可视化工具支持 IEnumerable 集合，其中对象类型 (T) 可以是简单类型或复杂类型（如字典）。

## <a name="open-the-visualizer"></a>打开可视化工具

要打开表可视化工具，必须在调试期间暂停。

1. 如果你有 IEnumerable 代码实现，请找到放大镜图标 ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")：

   - “局部变量”和“监视窗口”的值列。
   - 将鼠标悬停在一个变量上时，

1. 选择该图标以打开 IEnumerable 表可视化工具。

   :::image type="content" source="../debugger/media/vs-2022/dbg-open-table-visualizer.png" alt-text="打开表可视化工具":::

## <a name="view-table-visualizer-data"></a>查看表可视化工具数据

可视化工具以表格式显示 IEnumerable 数据。

:::image type="content" source="../debugger/media/vs-2022/dbg-table-visualizer.png" alt-text="查看可视化工具数据":::

可使用右键单击上下文菜单自定义视图：

- 选择“隐藏列”以隐藏重复数据。
- 选择“展开列”以查看复杂数据中更深入的项。
- 选择“隐藏子级”以获取更简洁的数据视图。

## <a name="see-also"></a>请参阅

- [创建自定义可视化工具（C#、Visual Basic）](../debugger/create-custom-visualizers-of-data.md)