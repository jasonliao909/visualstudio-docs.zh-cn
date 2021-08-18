---
title: 如何：使用数据库中的数据填充工作表
description: 了解如何使用解决方案中对象中的数据，以及如何使用 Windows 窗体控件在工作表中显示数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets [Office development in Visual Studio], populating
- databases [Office development in Visual Studio], populating worksheets
- data [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: cd48feecfd100fc54748511107094bf1351c8c4d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046771"
---
# <a name="how-to-populate-worksheets-with-data-from-a-database"></a>如何：使用数据库中的数据填充工作表

可以使用与访问窗体项目中Office相同的方式访问文档级Windows数据。 使用相同的工具和代码将数据引入解决方案，然后即可使用 Windows 窗体控件来显示该数据。 此外，可以利用称为宿主控件的控件，这些控件是Microsoft Office Excel事件和数据绑定功能增强的本机对象。 有关详细信息，请参阅主机 [项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

[!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

下列示例演示了如何使用设计器在文档级项目中添加数据绑定控件。 有关如何运行时在应用程序级项目中添加数据绑定控件的示例，请参阅演练[：VSTO外接程序项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)。

## <a name="add-a-data-bound-control-to-a-worksheet-at-design-time"></a>在设计时向工作表添加数据绑定控件

### <a name="to-populate-a-worksheet-with-data-from-a-database"></a>使用数据库中的数据填充工作表

1. 在 Excel打开一个文档级Visual Studio，在设计器中打开工作表。

2. 打开“数据源”  窗口并为项目创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

3. 将"数据源"窗口中的字段 **或表** 拖动到工作表。

在工作表上创建以下控件之一：

- 如果拖动字段，则 <xref:Microsoft.Office.Tools.Excel.NamedRange> 工作表上会创建一个控件。 有关详细信息，请参阅 [NamedRange 控件](../vsto/namedrange-control.md)。

- 如果拖动表，则 <xref:Microsoft.Office.Tools.Excel.ListObject> 工作表上会创建一个控件。 有关详细信息，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

可以通过在"数据源"窗口中选择表或字段，然后从下拉列表中选择其他控件来添加其他控件。

## <a name="objects-in-the-project"></a>项目中的对象

除了该控件，还会自动将以下数据相关的对象添加到你的项目：

- 一个类型化数据集，它会封装数据库中你连接到的数据表。 有关详细信息，请参阅 数据集[中的数据集Visual Studio。](../data-tools/dataset-tools-in-visual-studio.md)

- 一个 <xref:System.Windows.Forms.BindingSource>，它将控件连接到类型化数据集。 有关详细信息，请参阅 [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)。

- 将类型数据集连接到数据库的 TableAdapter。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

- TableAdapterManager，用于协调数据集中的表适配器以启用分层更新。 有关详细信息，请参阅分层 [更新和](../data-tools/hierarchical-update.md) [TableAdapterManager 参考](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference)。

运行项目时，该控件将显示数据源中的第一条记录。 可以借助 <xref:System.Windows.Forms.BindingSource> 来使用户能滚动显示各个记录。

### <a name="to-scroll-through-the-records"></a>滚动显示记录

- 使用 <xref:System.Windows.Forms.BindingSource> 方法，如 <xref:System.Windows.Forms.BindingSource.MoveNext%2A> 和 <xref:System.Windows.Forms.BindingSource.MovePrevious%2A>。

若要了解如何向类型数据集和数据库发送更新，请参阅如何：使用主机控件 中的数据 [更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

## <a name="see-also"></a>请参阅

- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [如何：使用 对象的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：使用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：使用服务数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)
- [如何：使用来自主机控件的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)