---
title: 向 n 层应用程序中的数据集添加代码
description: 在 Visual Studio 中，将代码添加到 n 层应用中的数据集。 为数据集创建一个分部类文件并向其添加代码（而不是向 DatasetName.Dataset.Designer）。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601245"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

可以通过为数据集创建分部类文件并向其添加代码（而不是向 DatasetName.Dataset.Designer 文件添加代码）来扩展数据集的功能。 分部类使特定类的代码可以在多个物理文件之间划分。 有关详细信息，请参阅[分部](/dotnet/visual-basic/language-reference/modifiers/partial)或[分部类和方法](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

每次对数据集定义进行更改时（在类型化数据集中）都会生成定义数据集的代码。 在运行任何向导时进行修改数据集配置的更改时，也会生成此代码。 若要防止在重新生成数据集的过程中删除代码，请将代码添加到数据集的分部类文件。

默认情况下，分离数据集和 TableAdapter 代码后，结果是在每个项目中生成离散类文件。 原始项目有一个名为 DatasetName.Designer.vb（或 DatasetName.Designer.cs）的文件，其中包含 TableAdapter 代码 。 Dataset Project 属性中指定的项目有一个名为 DatasetName.DataSet.Designer.vb（或 DatasetName.DataSet.Designer.cs）的文件。此文件包含数据集代码 。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类。 你必须手动将它们移到数据集项目中。

> [!NOTE]
> 该类型化数据集提供了在需要添加验证代码时生成 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件处理程序的功能。 有关详细信息，请参阅[向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

1. 找到包含 .xsd 文件的项目。

2. 选择 .xsd 文件以打开数据集。

3. 右键单击要向其添加代码的数据表（标题栏中的表名），然后选择“查看代码”。

     将创建一个分部类并在代码编辑器中打开它。

4. 将代码添加到分部类声明中。

     下面的示例演示在 NorthwindDataSet 中将代码添加到 CustomersDataTable 的位置：

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

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 n 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
