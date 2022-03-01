---
title: 代码度量窗口
ms.date: 12/12/2017
description: 了解如何查看、筛选、重新排列和导出 Visual Studio 代码度量分析数据。 查看如何基于代码度量结果创建工作项。
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
ms.openlocfilehash: 6df7716aaf4eedcdb48031b95d8ff43006f83eba
ms.sourcegitcommit: 169b7b66d13b7e3c86097b42206dd33389cd9166
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2022
ms.locfileid: "138148890"
---
# <a name="use-the-code-metrics-results-window"></a>使用“代码度量结果”窗口

“代码度量结果”窗口显示由代码度量分析所生成的数据。 若要详细了解代码度量数据值，请参阅[代码度量值](../code-quality/code-metrics-values.md)。

## <a name="display-code-metrics-results"></a>显示代码度量结果

生成代码度量结果时，会自动显示“代码度量结果”窗口。 也可随时显示此窗口。

可按下列菜单序列之一显示“代码度量结果”窗口：

- 在“分析”菜单中，选择“窗口” > 代码度量结果”  。

- 在“视图”菜单，选择“其他窗口” > “代码度量结果”  。

即使不包含任何结果，也会打开“代码度量结果”窗口。

### <a name="to-view-code-metrics-details"></a>查看代码度量详细信息

如果已生成代码度量结果，请在“层次结构”列中展开树。

## <a name="filter-code-metrics-results"></a>筛选代码度量结果

可使用顶部的工具栏筛选“代码度量结果”窗口中显示的结果。 例如，你可能只想查看可维护性指数小于 65 的结果。

“筛选器”下拉菜单包含结果列的名称。 定义筛选器后，会将其添加到列表的底部，并同时添加缩进。 该列表可包含已定义的最后 10 个筛选器。

### <a name="to-filter-the-code-metrics-results"></a>筛选代码度量结果

1. 从“筛选器”列表选择列名称。

2. 在“最小值”中，键入要显示的最小值。

3. 在“最大值”中，键入要显示的最大值。

4. 单击“应用筛选器”按钮。

5. 若要查看结果详细信息，请展开层次结构树。

## <a name="add-remove-and-rearrange-data-columns"></a>添加、删除和重新排列数据列

可从“代码度量结果”窗口中添加或删除结果列。 此外，还可重新排列结果列，使其按你需要的顺序显示。

### <a name="add-or-remove-a-column"></a>添加或删除列

1. 单击“添加/删除列”按钮，或者右键单击任意列标题，然后单击“添加/删除列” 。

1. 在“添加/删除列”对话框中，选中或清除要添加或删除的列对应的复选框，然后选择“确定” 。

### <a name="rearrange-columns"></a>对列进行重新排列

1. 单击“添加/删除列”按钮。

1. 在“添加/删除列”对话框中，选中或清除要移动的列，然后选择向上箭头或向下箭头。

1. 当列在所需位置时，选择“确认”。

## <a name="copy-data-to-the-clipboard-or-excel"></a>将数据复制到剪贴板或 Excel

可选择一行代码度量数据，并将所选的行复制到剪贴板，用作包含每个数据列的一行名称和值的文本字符串。 还可单击“在 Microsoft Excel 中打开所选内容”，将所有代码度量结果导出到 Excel 电子表格。

## <a name="create-a-work-item-based-on-code-metric-results"></a>基于代码度量结果创建工作项

可创建基于“代码度量结果”窗口中的结果的 [Azure Boards](/azure/devops/boards/index?view=vsts&preserve-view=true) 工作项。 创建工作项后，Visual Studio 会在“标题”字段中自动输入一个标题，在“历史记录”选项卡下自动输入代码度量数据 。

有关 Azure Boards 工作项的详细信息，请参阅[工作项](/azure/devops/boards/work-items/about-work-items)。

### <a name="to-create-a-work-item-based-on-a-result"></a>基于结果创建工作项

1. 右键单击结果。

2. 指向“创建工作项”，然后单击要创建的工作项类型（Bug、任务等）  。

3. 填写所有必填字段，完成工作项窗体。

4. 在“文件”菜单上，单击“全部保存”以保存项目 。

### <a name="to-create-a-bug-based-on-a-result"></a>基于结果创建 bug

1. 单击结果将其选中。

2. 单击“创建工作项”按钮。

3. 填写所有必填字段，完成工作项窗体。

4. 在“文件”菜单上，单击“全部保存”以保存项目 。

## <a name="see-also"></a>另请参阅

- [代码度量值](../code-quality/code-metrics-values.md)
- [如何：生成代码度量数据](../code-quality/how-to-generate-code-metrics-data.md)
