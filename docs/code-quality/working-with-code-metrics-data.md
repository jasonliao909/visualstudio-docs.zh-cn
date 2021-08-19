---
title: "\"代码指标\"窗口"
ms.date: 12/12/2017
description: 了解如何查看、筛选、重新排列和导出Visual Studio指标分析数据。 了解如何基于代码指标结果创建工作项。
ms.custom: SEO-VS-2020
ms.topic: reference
f1_keywords:
- vs.codemetrics.output
helpviewer_keywords:
- code metrics results
- code metrics results window
- results window, code metrics
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-code-analysis
ms.workload:
- multiple
ms.openlocfilehash: 316f03d737f2e7d294eb5d743496652f8635d58d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122113947"
---
# <a name="use-the-code-metrics-results-window"></a>使用"代码指标结果"窗口

" **代码指标结果** "窗口显示由代码指标分析生成的数据。 有关代码指标数据值的信息，请参阅 [代码指标值](../code-quality/code-metrics-values.md)。

## <a name="display-code-metrics-results"></a>显示代码指标结果

生成 **代码指标结果** 时，将自动显示"代码指标结果"窗口。 还可以随时显示窗口。

可以使用以下菜单序列之一显示"代码指标结果"窗口：

- 在"**分析"** 菜单上 **，Windows"**  >  **代码指标结果"。**

- 在"视图 **"** 菜单上，选择 **"其他** Windows  >  **代码指标结果"。**

" **代码指标结果"** 窗口将打开，即使不包含任何结果。

### <a name="to-view-code-metrics-details"></a>查看代码指标详细信息

如果已生成代码指标结果，请展开"层次结构" **列中的** 树。

## <a name="filter-code-metrics-results"></a>筛选代码指标结果

可以使用顶部的工具栏筛选"代码指标结果"窗口中显示的结果。 例如，你可能只想查看可维护性索引低于 65 的结果。

" **筛选器** "下拉框包含结果列的名称。 定义筛选器后，它会与缩进一起添加到列表底部。 该列表可以包含最后定义的 10 个筛选器。

### <a name="to-filter-the-code-metrics-results"></a>筛选代码指标结果

1. 从" **筛选器** "列表中，选择列名称。

2. 在 **"最小值**"中，键入要显示的最小值。

3. 在 **"** 最大值"中，键入要显示的最大值。

4. 单击" **应用筛选器"** 按钮。

5. 若要查看结果详细信息，请展开层次结构树。

## <a name="add-remove-and-rearrange-data-columns"></a>添加、删除和重新排列数据列

可以在"代码指标结果"窗口中 **添加或删除结果** 列。 此外，还可以重新排列结果列，以便它们按你预期的顺序显示。

### <a name="add-or-remove-a-column"></a>添加或删除列

1. 单击"**添加/删除列"** 按钮，或右键单击任何列标题，然后单击"**添加/删除列"。**

1. 在"**添加/删除列**"对话框中，选中或清除要添加或删除的列的复选框，然后选择"确定 **"。**

### <a name="rearrange-columns"></a>重新排列列

1. 单击" **添加/删除列"** 按钮。

1. 在" **添加/删除列** "对话框中，选择要移动的列，然后选择向上箭头或向下箭头。

1. 当列定位到需要的位置时，选择"确定 **"。**

## <a name="copy-data-to-the-clipboard-or-excel"></a>将数据复制到剪贴板或Excel

可以选择一行选定的代码指标数据，并作为文本字符串复制到剪贴板，该字符串包含每个数据列的名称和值的一行。 还可以 **单击"在** Microsoft Excel选择"，将所有代码指标结果导出到Excel电子表格。

## <a name="create-a-work-item-based-on-code-metric-results"></a>基于代码指标结果创建工作项

可以在"代码 [Azure Boards](/azure/devops/boards/index?view=vsts&preserve-view=true)结果"窗口中创建一个基于结果 **的** 工作项。 创建工作项时，Visual Studio"标题"字段中自动输入标题，在"历史记录"选项卡下输入 **代码指标** 数据。

有关工作项Azure Boards，请参阅[工作项](/azure/devops/boards/work-items/index?view=vsts&preserve-view=true)。

### <a name="to-create-a-work-item-based-on-a-result"></a>基于结果创建工作项

1. 右键单击结果。

2. 指向 **"创建工作项"，** 然后单击要创建的工作项 (**Bug、** 任务等) 。 

3. 填写所有必填字段，完成工作项窗体。

4. 在" **文件"** 菜单上，单击 **"** 全部保存"以保存工作项。

### <a name="to-create-a-bug-based-on-a-result"></a>基于结果创建 bug

1. 单击结果将其选中。

2. 单击" **创建工作项"** 按钮。

3. 填写所有必填字段，完成工作项窗体。

4. 在" **文件"** 菜单上，单击 **"** 全部保存"以保存工作项。

## <a name="see-also"></a>请参阅

- [代码指标值](../code-quality/code-metrics-values.md)
- [如何：生成代码指标数据](../code-quality/how-to-generate-code-metrics-data.md)
