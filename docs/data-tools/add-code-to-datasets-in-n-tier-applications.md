---
title: 向 n 层应用程序中的数据集添加代码
description: 向 Visual Studio 中的 n 层应用中的数据集添加Visual Studio。 为数据集创建分部类文件，并添加代码 (而不是 DatasetName.Dataset.Designer) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending DataSets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 7df5c2fd963ce628f146bde5b8df754866898b20
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122134813"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

可以通过为数据集创建分部类文件并添加代码来扩展数据集的功能 (而不是将代码添加到 *DatasetName*。Dataset.Designer 文件) 。 分部类允许特定类的代码在多个物理文件之间划分。 有关详细信息，请参阅[分部或](/dotnet/visual-basic/language-reference/modifiers/partial)[分部类和方法](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

每次对类型数据集中的数据集定义 (更改时，都会生成定义数据集) 。 在运行修改数据集配置的任何向导期间进行更改时，也会生成此代码。 若要防止在重新生成数据集期间删除代码，请向数据集的分部类文件添加代码。

默认情况下，将数据集和 TableAdapter 代码分开后，结果是每个项目中的一个离散类文件。 原始项目具有名为 *DatasetName.Designer.vb* (*或 DatasetName.Designer.cs*) 包含 TableAdapter 代码的文件。 **在 DataSet Project** 属性中指定的项目具有名为 *DatasetName.DataSet.Designer.vb* (或 *DatasetName.DataSet.Designer.cs*) 的文件。此文件包含数据集代码。

> [!NOTE]
> 通过设置 DataSet Project 属性 (**DataSet** 和 TableAdapters) 时，不会自动移动项目中的现有分部数据集类。 必须将现有数据集分部类手动移动到数据集项目。

> [!NOTE]
> 需要添加验证代码时，类型数据集提供生成和事件处理程序 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 的功能。 有关详细信息，请参阅向 [n 层数据集 添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>将代码添加到 n 层应用程序中的 DataSet

1. 找到包含 *.xsd 文件* 的项目。

2. 选择 **.xsd** 文件以打开数据集。

3. 右键单击要向其中添加代码的数据表 (标题栏中的表名称，然后选择"查看 **) "。**

     分部类在代码编辑器中创建并打开。

4. 在分部类声明中添加代码。

     以下示例显示将代码添加到 NorthwindDataSet 中的 CustomersDataTable 的何处：

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 n 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
- [数据集工具Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)
