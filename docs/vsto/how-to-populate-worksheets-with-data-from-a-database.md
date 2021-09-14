---
title: 如何：用数据库中的数据填充工作表
description: 了解如何使用解决方案中对象的数据，以及如何使用 Windows 窗体控件来显示工作表中的数据。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664738"
---
# <a name="how-to-populate-worksheets-with-data-from-a-database"></a>如何：用数据库中的数据填充工作表

您可以访问文档级 Office 项目中的数据，其方式与访问 Windows 窗体项目中的数据的方式相同。 使用相同的工具和代码将数据引入解决方案，然后即可使用 Windows 窗体控件来显示该数据。 此外，可以利用称为 "宿主控件" 的控件，这些控件是使用事件和数据绑定功能增强 Microsoft Office Excel 中的本机对象。 有关详细信息，请参阅 [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

[!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

下列示例演示了如何使用设计器在文档级项目中添加数据绑定控件。 有关如何在运行时在应用程序级项目中添加数据绑定控件的示例，请参阅[演练： VSTO 外接程序项目中的复杂数据绑定](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)。

## <a name="add-a-data-bound-control-to-a-worksheet-at-design-time"></a>在设计时将数据绑定控件添加到工作表

### <a name="to-populate-a-worksheet-with-data-from-a-database"></a>用数据库中的数据填充工作表

1. 在 Visual Studio 中打开 Excel 文档级项目，并在设计器中打开工作表。

2. 打开“数据源”  窗口并为项目创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

3. 将所需的字段或表从 " **数据源** " 窗口拖到工作表中。

在工作表上创建以下控件之一：

- 如果拖动某个字段，则 <xref:Microsoft.Office.Tools.Excel.NamedRange> 会在工作表上创建一个控件。 有关详细信息，请参阅 [NamedRange 控件](../vsto/namedrange-control.md)。

- 如果拖动某个表，则 <xref:Microsoft.Office.Tools.Excel.ListObject> 会在工作表上创建一个控件。 有关详细信息，请参阅 [ListObject 控件](../vsto/listobject-control.md)。

您可以通过在 " **数据源** " 窗口中选择表或字段，然后从下拉列表中选择其他控件来添加不同的控件。

## <a name="objects-in-the-project"></a>项目中的对象

除了该控件，还会自动将以下数据相关的对象添加到你的项目：

- 一个类型化数据集，它会封装数据库中你连接到的数据表。 有关详细信息，请参阅[Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)。

- 一个 <xref:System.Windows.Forms.BindingSource>，它将控件连接到类型化数据集。 有关详细信息，请参阅 [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)。

- 将类型化的数据集连接到数据库的 TableAdapter。 有关详细信息，请参阅 [TableAdapter 概述](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview)。

- TableAdapterManager，用于在数据集中协调表适配器以启用分层更新。 有关详细信息，请参阅 [分层更新](../data-tools/hierarchical-update.md) 和 [TableAdapterManager 参考](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference)。

运行项目时，该控件将显示数据源中的第一条记录。 可以借助 <xref:System.Windows.Forms.BindingSource> 来使用户能滚动显示各个记录。

### <a name="to-scroll-through-the-records"></a>滚动显示记录

- 使用 <xref:System.Windows.Forms.BindingSource> 方法，如 <xref:System.Windows.Forms.BindingSource.MoveNext%2A> 和 <xref:System.Windows.Forms.BindingSource.MovePrevious%2A>。

有关如何将更新发送到类型化数据集和数据库的信息，请参阅 [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

## <a name="see-also"></a>另请参阅

- [在 Office 解决方案中将数据绑定到控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [如何：用对象中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：用数据库中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [如何：用服务中的数据填充文档](../vsto/how-to-populate-documents-with-data-from-services.md)
- [如何：使用主机控件中的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)