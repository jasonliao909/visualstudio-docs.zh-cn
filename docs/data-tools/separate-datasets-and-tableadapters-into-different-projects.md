---
title: 使用单独的项目错误
description: 了解如何将数据集和 Tableadapter 分离到不同的项目中，以便快速分离应用程序层并生成 N 层数据应用程序。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601094"
---
# <a name="separate-datasets-and-tableadapters-into-different-projects"></a>将数据集和 TableAdapter 分离到不同的项目中
类型化数据集经过改进，现在可以在独立的项目中生成 [TableAdapter](create-and-configure-tableadapters.md) 和数据集类。 这使你能够快速分离各应用程序层及生成 N 层数据应用程序。

下面的过程描述了使用数据集设计器将数据集代码生成到一个项目中的过程，该项目与包含生成的 TableAdapter 代码的项目是分离的。

## <a name="separate-datasets-and-tableadapters"></a>分离数据集和 TableAdapter
将数据集代码与 TableAdapter 代码分离时，包含数据集代码的项目必须位于当前解决方案中。 如果此项目不在当前解决方案中，则无法在“属性”窗口中“数据集项目”列表中找到该项目 。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

#### <a name="to-separate-the-dataset-into-a-different-project"></a>将数据集分离到不同的项目中

1. 打开包含数据集（.xsd 文件）的解决方案。

    > [!NOTE]
    > 如果解决方案不包含要将数据集代码分离到其中的项目，请创建该项目，或者将现有项目添加到解决方案中。

2. 在“解决方案资源管理器”中双击类型化数据集文件（.xsd 文件），以在“数据集设计器”中打开该数据集。

3. 选择数据集设计器的空白区域。

4. 在“属性”窗口中找到“数据集项目”节点 。

5. 在“数据集项目”列表中，选择要在其中生成数据集代码的项目的名称。

     选择要在其中生成数据集代码的项目后，将使用默认文件名填充“数据集文件”属性。 如果需要，可以更改此名称。 此外，如果想要将数据集代码生成到特定目录中，则可以将“项目文件夹”属性设置为文件夹的名称。

    > [!NOTE]
    > 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，不会自动移动项目中现有的数据集分部类。 必须手动将现有的分部数据集类移动到数据集项目。

6. 保存数据集。

     数据集代码生成到“数据集项目”属性中选定的项目，并且 TableAdapter 代码生成到当前项目中 。

默认情况下，分离数据集和 TableAdapter 代码后，结果是在每个项目中生成离散类文件。 原始项目有一个名为 DatasetName.Designer.vb（或 DatasetName.Designer.cs）的文件，其中包含 TableAdapter 代码 。 “数据集项目”属性中指定的项目有一个名为 DatasetName.DataSet.Designer.vb（或 DatasetName.DataSet.Designer.cs）的文件，其中包含数据集代码 。

> [!NOTE]
> 若要查看生成的类文件，请选择数据集或 TableAdapter 项目。 然后在“解决方案资源管理器”中，选择“显示所有文件” 。

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [ADO.NET](/dotnet/framework/data/adonet/index)
