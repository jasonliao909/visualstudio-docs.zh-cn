---
title: 如何：使用数据库中的数据填充文档
description: 了解如何在解决方案中使用数据库中的数据，以及如何Windows窗体控件在文档中显示数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents, populating with data
- data, adding to documents
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: a2c49f7f40d7b73ed0db14e227ac97f8aacc7fca
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602274"
---
# <a name="how-to-populate-documents-with-data-from-a-database"></a>如何：使用数据库中的数据填充文档

可以用访问 Windows 窗体项目中的数据的相同方式来访问 Microsoft Office 文档级项目中的数据。 使用相同的工具和代码将数据从数据库引入解决方案，然后即可使用 Windows 窗体控件来显示该数据。

此外，还可以使用主机控件来显示数据。 主机控件是指 Microsoft Office Word 中借助事件和数据绑定容量进行增强的本地对象。 有关详细信息，请参阅主机 [项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

[!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

下列示例演示了如何使用设计器在文档级项目中添加数据绑定控件。 有关如何运行时在 VSTO 外接程序项目中添加数据绑定控件的示例，请参阅演练[：VSTO外接程序项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)。

![视频链接](../vsto/media/playvideo.gif "链接到视频")有关相关视频演示，请参阅将数据绑定到 Word 2007 内容控件 Using [Visual Studio Tools for the Office system (3.0) 。 ](/previous-versions/office/developer/office-2007/bb967663(v=office.12))

## <a name="add-a-control-to-a-document-at-design-time"></a>在设计时向文档添加控件

### <a name="to-populate-a-document-with-data-from-a-database"></a>使用数据库的数据填充文档

1. 当文档在设计器中打开时，打开 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中 Word 文档级项目。

2. 打开 **"数据源"** 窗口，从数据库创建数据源。 有关详细信息，请参阅 [添加新连接](../data-tools/add-new-connections.md)。

3. 将"数据源"窗口中 **的字段** 拖到文档中。

将内容控件添加到了该文档。 内容控件的类型取决于所选字段的数据类型。 有关详细信息，请参阅内容 [控件](../vsto/content-controls.md)。

可以通过在"数据源"窗口中选择数据字段，然后从下拉列表中选择其他控件来添加其他控件。

## <a name="objects-in-the-project"></a>项目中的对象

除了该控件，还会自动将以下数据相关的对象添加到你的项目：

- 一个类型化数据集，它会封装数据库中你连接到的数据表。 有关详细信息，请参阅 中的[数据集Visual Studio。](../data-tools/dataset-tools-in-visual-studio.md)

- 一个 <xref:System.Windows.Forms.BindingSource>，它将控件连接到类型化数据集。 有关详细信息，请参阅 [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)。

- 将类型数据集连接到数据库的 TableAdapter。 有关详细信息，请参阅创建 [和配置 TableAdapters](../data-tools/create-and-configure-tableadapters.md)。

- TableAdapterManager，用于协调数据集中的表适配器以启用分层更新。 有关详细信息，请参阅分层 [更新和](../data-tools/hierarchical-update.md) [TableAdapterManager 参考](../data-tools/fill-datasets-by-using-tableadapters.md#tableadaptermanager-reference)。

运行项目时，该控件将显示数据源中的第一条记录。 可以借助 <xref:System.Windows.Forms.BindingSource> 来使用户能滚动显示各个记录。

### <a name="to-scroll-through-the-records"></a>滚动显示记录

- 使用 <xref:System.Windows.Forms.BindingSource> 方法，如 <xref:System.Windows.Forms.BindingSource.MoveNext%2A> 和 <xref:System.Windows.Forms.BindingSource.MovePrevious%2A>。

若要了解如何向类型数据集和数据库发送更新，请参阅如何：使用主机控件 中的数据 [更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)。

## <a name="see-also"></a>另请参阅

- [将数据绑定到解决方案中的Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)
- [添加新数据源](../data-tools/add-new-data-sources.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [如何：使用 对象的数据填充文档](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [如何：使用来自主机控件的数据更新数据源](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [在解决方案概述Office本地数据库文件](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)