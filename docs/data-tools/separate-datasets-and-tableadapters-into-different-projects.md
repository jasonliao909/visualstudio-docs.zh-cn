---
title: 使用单独的项目错误
description: 了解如何将数据集和 TableAdapters 分离到不同的项目中，以便快速分离应用程序层并生成 N 层数据应用程序。
ms.date: 11/04/2016
ms.topic: how-to
ms.custom: SEO-VS-2020
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, separating Datasets and TableAdapters
ms.assetid: f66a3940-6227-46af-a930-9177f425f4fd
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 335f6d1ab4a7dba28609a267e6a6ce950cb607ff
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122161819"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>将数据集和 TableAdapter 分离到不同的项目中
类型数据集已增强，因此 [可以将 TableAdapters](create-and-configure-tableadapters.md) 和数据集类生成到单独的项目中。 这使你可以快速分离应用程序层并生成 n 层数据应用程序。

以下过程描述使用 数据集设计器 将数据集代码生成到与包含生成的 TableAdapter 代码的项目分开的项目中的过程。

## <a name="separate-datasets-and-tableadapters"></a>单独的数据集和 TableAdapters
将数据集代码与 TableAdapter 代码分开时，包含数据集代码的项目必须位于当前解决方案中。 如果此项目不在当前解决方案中，它将在"属性"窗口中的"**数据集** Project **列表中** 不可用。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>将数据集分隔为不同的项目

1. 打开包含 *.xsd* (数据集的解决方案) 。

    > [!NOTE]
    > 如果解决方案不包含要分隔数据集代码的项目，请创建项目，或将现有项目添加到解决方案。

2. 双击键入的数据集文件 (*中的 .xsd*) ，解决方案资源管理器打开 数据集设计器 中的 **数据集**。

3. 选择的空白区域 **数据集设计器。**

4. 在"**属性"** 窗口中，找到 **"数据集** Project节点。

5. 在 **"数据集Project** 列表中，选择要生成数据集代码的项目的名称。

     选择要生成数据集代码的项目后，" **数据集** 文件"属性将填充默认文件名。 如有必要，可以更改此名称。 此外，如果要将数据集代码生成到特定目录中，可以将 Project **Folder** 属性设置为文件夹的名称。

    > [!NOTE]
    > 通过设置 **DataSet** Project 属性 (将数据集和 TableAdapters) ，项目中的现有分部数据集类不会自动移动。 必须将现有分部数据集类手动移动到数据集项目。

6. 保存数据集。

     数据集代码将生成到 **DataSet** Project属性中的选定项目中 **，TableAdapter** 代码将生成到当前项目中。

默认情况下，将数据集和 TableAdapter 代码分开后，结果是每个项目中的一个离散类文件。 原始项目具有名为 *DatasetName.Designer.vb* (*或 DatasetName.Designer.cs*) 包含 TableAdapter 代码的文件。 在 Dataset **Project** 属性中指定的项目具有名为 *DatasetName.DataSet.Designer.vb* (或 *DatasetName.DataSet.Designer.cs*) 的文件，其中包含数据集代码。

> [!NOTE]
> 若要查看生成的类文件，请选择数据集或 TableAdapter 项目。 然后 **，在解决方案资源管理器** 中，选择"**显示所有文件"。**

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)
