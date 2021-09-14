---
title: 向 n 层应用程序中的 TableAdapter 添加代码
description: 将代码添加到 n 层应用程序中的表适配器。 为 TableAdapter 创建分部类文件，并添加 (而不是 DatasetName.DataSet.Designer) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 55b6a64953944bacd8fcda73a9edeab00a99afc5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601240"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>向 n 层应用程序中的 TableAdapter 添加代码
可以通过为 TableAdapter 创建分部类文件并添加代码来扩展 TableAdapter 的功能 (而不是将代码添加到 *DatasetName.DataSet.Designer*) 。 分部类允许特定类的代码在多个物理文件之间划分。 有关详细信息，请参阅[Type](/dotnet/visual-basic/language-reference/modifiers/partial) ([部分) 。 ](/dotnet/csharp/language-reference/keywords/partial-type)

每次对数据集中的 TableAdapter 进行更改时，都会生成定义 TableAdapter 的代码。 在运行修改 TableAdapter 配置的任何向导期间进行更改时，也会生成此代码。 若要防止在重新生成 TableAdapter 期间删除代码，请向 TableAdapter 的分部类文件添加代码。

默认情况下，将数据集和 TableAdapter 代码分开后，结果是每个项目中的一个离散类文件。 原始项目具有名为 *DatasetName.Designer.vb* (*或 DatasetName.Designer.cs*) 包含 TableAdapter 代码的文件。 在 Dataset Project 属性 **中** 指定的项目具有名为 *DatasetName.DataSet.Designer.vb* (或 *DatasetName.DataSet.Designer.cs*) 的文件，其中包含数据集代码。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类。 必须将现有分部数据集类手动移动到数据集项目。

> [!NOTE]
> 数据集提供在需要验证时生成 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 和事件处理程序的功能。 有关详细信息，请参阅向 [n 层数据集 添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>将用户代码添加到 n 层应用程序中的 TableAdapter

1. 找到包含 *.xsd 文件* 的项目。

2. 双击 *.xsd* 文件以 **打开数据集设计器。**

3. 右键单击要添加代码的 TableAdapter，然后选择"查看 **代码"。**

     分部类在代码编辑器中创建并打开。

4. 在分部类声明中添加代码。

5. 以下示例显示将代码添加到 `CustomersTableAdapter` 中的 位置 `NorthwindDataSet` ：

    ```vb
    Partial Public Class CustomersTableAdapter
        ' Add code here to add functionality
        ' to the CustomersTableAdapter.
    End Class
    ```

    ```csharp
    public partial class CustomersTableAdapter
    {
        // Add code here to add functionality
        // to the CustomersTableAdapter.
    }
    ```

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 n 层应用程序中的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
