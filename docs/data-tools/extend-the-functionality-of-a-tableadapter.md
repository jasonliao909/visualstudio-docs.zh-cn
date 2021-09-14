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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601162"
---
# <a name="extend-the-functionality-of-a-tableadapter"></a>扩展 TableAdapter 的功能

可以通过将代码添加到 TableAdapter 的分部类文件来扩展 TableAdapter 的功能。

对 **数据集设计器** 中的 TableAdapter 进行任何更改时，或者当向导修改 tableadapter 的配置时，将重新生成定义 tableadapter 的代码。 若要防止在重新生成 TableAdapter 时删除代码，请将代码添加到 TableAdapter 的分部类文件中。

分部类允许在多个物理文件之间划分特定类的代码。 有关详细信息，请参阅 [部分](/dotnet/visual-basic/language-reference/modifiers/partial) 或 [部分 (类型) ](/dotnet/csharp/language-reference/keywords/partial-type)。

## <a name="locate-tableadapters-in-code"></a>在代码中找到 Tableadapter

尽管 Tableadapter 是用 **数据集设计器** 设计的，但生成的 TableAdapter 类并不是的嵌套类 <xref:System.Data.DataSet> 。 TableAdapter 位于基于 TableAdapter 关联数据集的名称的命名空间中。 例如，如果应用程序包含名为的数据集 `HRDataSet` ，则 tableadapter 将位于 `HRDataSetTableAdapters` 命名空间中。  (命名约定遵循此模式： *DatasetName*  +  `TableAdapters`) 。

下面的示例假定名为 `CustomersTableAdapter` 的 TableAdapter 与 `NorthwindDataSet` 一起位于项目中。

### <a name="to-create-a-partial-class-for-a-tableadapter"></a>为 TableAdapter 创建分部类

1. 转到 " **Project** " 菜单并选择 "**添加类**"，将新类添加到项目。

2. 命名类 `CustomersTableAdapterExtended`。

3. 选择 **添加** 。

4. 将代码替换为项目的正确命名空间和分部类名称，如下所示：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/CustomersTableAdapterExtended.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/CustomersTableAdapterExtended.vb" id="Snippet2":::

## <a name="see-also"></a>另请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
