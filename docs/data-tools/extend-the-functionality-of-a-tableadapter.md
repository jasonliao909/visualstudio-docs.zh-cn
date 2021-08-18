---
title: 扩展 TableAdapter 的功能
description: 了解如何通过将代码添加到 TableAdapter 的分部类文件来扩展 TableAdapter 的功能。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- data [Visual Studio], extending TableAdapters
- TableAdapters, adding functionality
ms.assetid: 418249c8-c7f3-47ef-a94c-744cb6fe6aaf
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 29c7d9924d822cabdb28c9d3048e457cd7b88d64
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122154870"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>扩展 TableAdapter 的功能

可以通过将代码添加到 TableAdapter 的分部类文件来扩展 TableAdapter 的功能。

如果对 数据集设计器 中的 TableAdapter 进行了任何更改，或者向导修改 TableAdapter **的配置，将重新生成** 定义 TableAdapter 的代码。 若要防止在重新生成 TableAdapter 期间删除代码，请向 TableAdapter 的分部类文件添加代码。

分部类允许特定类的代码在多个物理文件之间划分。 有关详细信息，请参阅 Type [ (](/dotnet/visual-basic/language-reference/modifiers/partial) [部分) 。 ](/dotnet/csharp/language-reference/keywords/partial-type)

## <a name="locate-tableadapters-in-code"></a>在代码中查找 TableAdapters

虽然 TableAdapter 是使用数据集设计器设计的，但生成的 TableAdapter 类不是 的嵌套类 <xref:System.Data.DataSet> 。 TableAdapter 位于基于 TableAdapter 关联数据集的名称的命名空间中。 例如，如果应用程序包含名为 的数据集 `HRDataSet` ，则 TableAdapters 将位于 `HRDataSetTableAdapters` 命名空间中。  (命名约定遵循以下模式 *：DatasetName*  +  `TableAdapters`) 。

下面的示例假定名为 `CustomersTableAdapter` 的 TableAdapter 与 `NorthwindDataSet` 一起位于项目中。

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>为 TableAdapter 创建分部类

1. 通过进入"新建"菜单并选择"添加类 **"，Project** 向 **项目添加新类**。

2. 命名类 `CustomersTableAdapterExtended`。

3. 选择 **添加**。

4. 将代码替换为项目的正确命名空间和分部类名称，如下所示：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/CustomersTableAdapterExtended.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/CustomersTableAdapterExtended.vb" id="Snippet2":::

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
