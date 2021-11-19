---
title: 数据集工具
description: 查看 Visual Studio 中可用的数据集工具。 了解数据集工作流、数据集和 N 层体系结构，以及数据集和 XML。
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
f1_keywords:
- vs.data.DataSet
helpviewer_keywords:
- untyped datasets
- datasets [Visual Basic], extended properties
- typed datasets
- current record in dataset
- XML [Visual Basic], datasets
- DataSet class, about datasets
- unique constraints (datasets)
- data relationships
- parent records in datasets
- extended properties, in typed datasets
- datasets [Visual Basic]
- schemas [Visual Basic], datasets
- datasets [Visual Basic], msprop
- master-detail tables, datasets
- databases [Visual Basic], updating
- msprop
- foreign keys, datasets
- DataSet class
- datasets [Visual Basic], filling
- case sensitivity, datasets
- constraints [Visual Basic], datasets
- child records
- related tables, datasets
- updating datasets, about dataset updates
- data caching, datasets
- DataRelation object, datasets
- untyped datasets, compared to typed datasets
- cache [Visual Studio], datasets
- datasets [Visual Basic], relationships
- related tables
- XML schemas, about XML schemas and datasets
- relationships, datasets
- typed datasets, compared to untyped datasets
- datasets [Visual Basic], populating
- datasets [Visual Basic], namespace
- data adapters, populating datasets
ms.assetid: ee57f4f6-9fe1-4e0a-be9a-955c486ff427
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 1e021a8ab30829aedd0a695a53993998e312ff81
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601170"
---
# <a name="dataset-tools-in-visual-studio"></a>Visual Studio 中的数据集工具

> [!NOTE]
> 数据集和相关类是 21 世纪初的旧版 .NET 技术，使应用程序能够在应用程序与数据库断开时处理内存中的数据。 它们对于使用户能够修改数据并持续更改回数据库的应用程序特别有用。 虽然数据集已被证明是一项非常成功的技术，但我们建议新的 .NET 应用程序使用实体框架。 实体框架提供了一种更自然的方式来将表格数据作为对象模型，并且具有更简单的编程接口。

`DataSet` 对象是内存中的对象，本质上是一个微型数据库。 它包含 `DataTable`、`DataColumn` 和 `DataRow` 对象，你可在其中存储和修改来自一个或多个数据库的数据，而无需维护打开的连接。 数据集维护有关其数据更改的信息，因此当应用程序重新连接时，可以跟踪更新并将其发送回数据库。

数据集和相关类在 .NET API 的 <xref:System.Data?displayProperty=fullName> 命名空间中定义。 可以使用 ADO.NET 动态地创建和修改代码中的数据集。 本部分中的文档演示如何使用 Visual Studio 设计器来处理数据集。 通过设计器创建的数据集使用 TableAdapter 对象与数据库进行交互。 以编程方式创建的数据集使用 DataAdapter 对象。 有关以编程方式创建数据集的信息，请参阅 [DataAdapters and DataReaders](/dotnet/framework/data/adonet/dataadapters-and-datareaders)。

如果应用程序只需要从数据库中读取数据，而不需要执行更新、添加或删除操作，则通常可以通过使用 `DataReader` 对象将数据检索到通用 `List` 对象或其他收集对象来获得更好的性能。 如果要显示数据，可以将用户界面数据绑定到集合。

## <a name="dataset-workflow"></a>数据集工作流

Visual Studio 提供了简化数据集处理的工具。 基本的端到端工作流是：

- 使用[“数据源”窗口](add-new-data-sources.md#data-sources-window)，可以从一个或多个数据源创建新的数据集。 使用“数据集设计器”配置数据集并设置其属性。 例如，需要指定要包含的数据源中的表以及每个表中的列。 仔细选择以节省数据集所需的内存量。 有关详细信息，请参阅[创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)。

- 指定表之间的关系，以便正确处理外键。 有关详细信息，请参阅[使用 TableAdapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)。

- 使用 TableAdapter 配置向导指定填充数据集的查询或存储过程，以及要实现的数据库操作（更新、删除等）。 有关详细信息，请参阅以下主题：

  - [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)

  - [编辑数据集中的数据](../data-tools/edit-data-in-datasets.md)

  - [验证数据集中的数据](../data-tools/validate-data-in-datasets.md)

  - [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)

- 查询和搜索数据集中的数据。 有关详细信息，请参阅[查询数据集](../data-tools/query-datasets.md)。 [!INCLUDE[linq_dataset](../data-tools/includes/linq_dataset_md.md)] 对 <xref:System.Data.DataSet> 对象中的数据启用 [LINQ（语言集成查询）](/dotnet/csharp/linq/)。 有关详细信息，请参阅 [LINQ to DataSet](/dotnet/framework/data/adonet/linq-to-dataset)。

- 使用“数据源”窗口将用户界面控件绑定到数据集或数据集的单个列，并指定用户可编辑的列。 有关详细信息，请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

## <a name="datasets-and-n-tier-architecture"></a>数据集和 N 层体系结构

有关 N 层应用程序中的数据集的信息，请参阅[在 n 层应用程序中使用数据集](../data-tools/work-with-datasets-in-n-tier-applications.md)。

## <a name="datasets-and-xml"></a>数据集和 XML

有关将数据集转换为 XML 或从 XML 转换数据集的信息，请参阅[将 XML 数据读入数据集](../data-tools/read-xml-data-into-a-dataset.md)和[将数据集另存为 XML](../data-tools/save-a-dataset-as-xml.md)。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
