---
title: 向 n 层应用程序中的 TableAdapter 添加代码
description: 向 n 层应用程序中的 table adapter 添加代码。 为 TableAdapter 创建一个分部类文件并向其（而不是向 DatasetName.DataSet.Designer）添加代码。
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
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601240"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>向 n 层应用程序中的 TableAdapter 添加代码
可以通过为 TableAdapter 创建分部类文件并向其添加代码（而不是向 DatasetName.DataSet.Designer 文件添加代码）来扩展 TableAdapter 的功能。 分部类使特定类的代码可以在多个物理文件之间划分。 有关详细信息，请参阅[分部](/dotnet/visual-basic/language-reference/modifiers/partial)或[分部（类型）](/dotnet/csharp/language-reference/keywords/partial-type)。

每次对数据集中的 TableAdapter 进行更改时，都会生成定义 TableAdapter 的代码。 在运行用于修改 TableAdapter 配置的任何向导期间进行更改时，也会生成此代码。 为防止代码在重新生成 TableAdapter 期间被删除，请将代码添加到 TableAdapter 的分部类文件中。

默认情况下，分离数据集和 TableAdapter 代码后，结果是每个项目中的离散类文件。 原始项目有一个名为 DatasetName.Designer.vb（或 DatasetName.Designer.cs）的文件，其中包含 TableAdapter 代码 。 Dataset Project 属性中指定的项目有一个名为 DatasetName.DataSet.Designer.vb（或 DatasetName.DataSet.Designer.cs）的文件，其中包含数据集代码 。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类。 必须手动将现有的分部数据集类移动到数据集项目。

> [!NOTE]
> 该数据集提供了在需要验证时生成 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件处理程序的功能。 有关详细信息，请参阅[向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>将用户代码添加到 n 层应用程序中的 TableAdapter

1. 找到包含 .xsd 文件的项目。

2. 双击 .xsd 文件以打开“数据集设计器”。

3. 右键单击要为其添加代码的 TableAdapter，然后选择“查看代码”。

     将创建一个分部类并在代码编辑器中打开它。

4. 将代码添加到分部类声明中。

5. 以下示例显示向 `NorthwindDataSet` 中的 `CustomersTableAdapter` 添加代码的位置：

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
