---
title: 创建和配置数据集
description: 在 Visual Studio 中创建和配置数据集。 数据集是一组 对象，用于将 DB 中的数据存储在内存中，并支持对该数据执行 CRUD 操作。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: how-to
helpviewer_keywords:
- typed datasets, creating
- datasets, creating
- datasets, configuring
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 8ce31c2e5a7e5e5f0441c213bd3f320212de5d3c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601189"
---
# <a name="how-to-create-and-configure-datasets-in-visual-studio"></a>如何：在 Visual Studio

数据集是一组对象，用于将数据库中的数据存储在内存中，并支持更改跟踪，以便对该数据启用创建、读取、更新和删除 (CRUD) 操作，而无需始终连接到数据库。 数据集专为数据业务 *应用程序的简单* 表单设计。 对于新应用程序，请考虑实体框架在内存中存储和建模数据。 若要使用数据集，应具备数据库概念的基本知识。

可以使用数据源配置向导 <xref:System.Data.DataSet> 在设计Visual Studio创建类型 **类**。 有关以编程方式创建数据集的信息，请参阅[使用](/dotnet/framework/data/adonet/dataset-datatable-dataview/creating-a-dataset) (ADO.NET) 。

## <a name="create-a-new-dataset-by-using-the-data-source-configuration-wizard"></a>使用数据源配置向导创建新数据集

1. 在 Visual Studio 中打开项目，然后选择Project"添加新数据源"以  >  **启动"数据源配置向导"。**

2. 选择要连接到的数据源的类型。

     ![数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)

3. 选择将成为数据集数据源的数据库。

     ![数据源选择连接](../data-tools/media/data-source-choose-a-connection.png)

4. 从要 (数据库) 、存储过程、函数和视图的表中选择表或单个列。

     ![选择数据库对象](../data-tools/media/raddata-chose-objects.png)

5. 单击“完成”  。

   数据集在 中 **显示为解决方案资源管理器。**

   ![数据集解决方案资源管理器](../data-tools/media/dataset-in-solution-explorer.png)

6. 单击数据集中的数据集 **解决方案资源管理器** 以在数据集设计器 **中打开数据集**。 数据集中的每个表都有一个关联的 对象 `TableAdapter` ，该对象在底部表示。 表适配器用于填充数据集，并选择性地将命令发送到数据库。

   ![数据集设计器](../data-tools/media/dataset-designer.png)

7. 连接表的关系线表示在数据库中定义的表关系。 默认情况下，数据库中的外键约束仅表示为关系，更新和删除规则设置为 none。 通常，这就是你需要的。 但是，可以单击这些行来打开"关系"对话框，可以在其中更改分层更新的行为。 有关详细信息，请参阅数据集[中的关系和](../data-tools/relationships-in-datasets.md)[分层更新](../data-tools/hierarchical-update.md)。

     !["数据集关系"对话框](../data-tools/media/raddata-relation-dialog.png)

8. 单击表中的表、表适配器或列名，在"属性"窗口中查看 **其** 属性。 可以在此处修改某些值。 只需记住，你正在修改数据集，而不是源数据库。

     ![数据集列属性](../data-tools/media/dataset-column-properties.png)

9. 可以将新表或表适配器添加到数据集，或为现有表适配器添加新查询，或者通过从"工具箱"选项卡拖动这些项来指定表 **之间的新** 关系。当数据集设计器位于焦点 **时，** 将显示此选项卡。

     ![数据集工具箱](../data-tools/media/raddata-dataset-toolbox.png)

接下来，可能需要指定如何使用数据填充数据集。 为此，请使用 **TableAdapter 配置向导**。 有关详细信息，请参阅使用 [TableAdapters](../data-tools/fill-datasets-by-using-tableadapters.md)填充数据集。

## <a name="add-a-database-table-or-other-object-to-an-existing-dataset"></a>将数据库表或其他对象添加到现有数据集

此过程演示如何从最初创建数据集时所使用的同一数据库中添加表。

1. 单击数据集中的数据集 **解决方案资源管理器，** 使 **数据集设计器** 成为焦点。

2. 单击 **资源页** 左边缘的"Visual Studio"选项卡，或在 **搜索** 框中键入数据源。

3. 右键单击数据集节点，然后选择"**使用向导配置数据源"。**

     ![数据源上下文菜单](../data-tools/media/data-source-context-menu.png)

4. 使用向导指定要添加到数据集的其他表、存储过程或其他数据库对象。

## <a name="add-a-stand-alone-data-table-to-a-dataset"></a>将独立数据表添加到数据集

1. 在“数据集设计器”中打开数据集。

2. 将类 <xref:System.Data.DataTable> 从"工具箱"**的"数据集**"选项卡拖到数据集设计器。 

3. 添加列以定义数据表。 右键单击表，然后选择"添加 **列**  >  **"。** 如有必要 **，** 可以使用"属性"窗口设置列的数据类型和键。

独立表需要在独立 `Fill` 表中实现逻辑，以便可以使用数据填充它们。 有关填充独立数据表的信息，请参阅 [从 DataAdapter](/dotnet/framework/data/adonet/populating-a-dataset-from-a-dataadapter)填充数据集。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
- [数据集中的关系](../data-tools/relationships-in-datasets.md)
- [分层更新](../data-tools/hierarchical-update.md)
- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
