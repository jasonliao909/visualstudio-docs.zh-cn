---
title: 在填充数据集时关闭约束
description: 了解如何在填充数据集时关闭约束。 以编程方式或通过使用数据集设计器暂停更新。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- DataRow.BeginEdit
- DataRow.EndEdit
- DataRow.CancelEdit
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, constraints
- constraints [Visual Basic], datasets
- datasets [Visual Basic], constraints
- constraints [Visual Basic], suspending during dataset update
ms.assetid: 553f7d0c-2faa-4c17-b226-dd02855bf1dc
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: ab5ff2fe9702d56ddc2c4b767ac40f3d63ddbe15
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601073"
---
# <a name="turn-off-constraints-while-filling-a-dataset"></a>在填充数据集时关闭约束

如果数据集包含约束（如外键约束），则它们可能会引发与针对数据集执行的操作的顺序相关的错误。 例如，在加载相关父记录之前加载子记录可能会违反约束并引发错误。 加载子记录后，约束会检查相关父记录并引发错误。

如果没有允许临时约束暂停的机制，则每次尝试将记录加载到子表中时都会引发错误。 暂停数据集中所有约束的另一种方式是使用 <xref:System.Data.DataRow.BeginEdit%2A> 和 <xref:System.Data.DataRow.EndEdit%2A> 属性。

> [!NOTE]
> 约束关闭时，不会引发验证事件（例如 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging>）。

## <a name="to-suspend-update-constraints-programmatically"></a>以编程方式暂停更新约束

- 以下示例演示如何暂时关闭数据集中的约束检查：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataEditing/CS/Form1.cs" id="Snippet10":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataEditing/VB/Form1.vb" id="Snippet10":::

## <a name="to-suspend-update-constraints-using-the-dataset-designer"></a>使用数据集设计器暂停更新约束

1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[演练：在数据集设计器中创建数据集](walkthrough-creating-a-dataset-with-the-dataset-designer.md)。

2. 在“属性”  窗口中，将 <xref:System.Data.DataSet.EnforceConstraints%2A> 属性设置为 `false`。

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
- [数据集中的关系](../data-tools/relationships-in-datasets.md)
