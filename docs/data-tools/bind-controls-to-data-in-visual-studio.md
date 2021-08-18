---
title: 将控件绑定到数据
description: 在 Visual Studio 中将控件绑定到数据。 通过从 "数据源" 窗口拖动项来创建数据绑定控件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: adbe3262e1da3c0d28f16bf32d94952c6565e142
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122081927"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将控件绑定到数据

通过将数据绑定到控件，可以向应用程序的用户显示数据。 您可以通过将 "**数据源**" 窗口中的项拖到设计图面上或 Visual Studio 的图面上的控件来创建这些数据绑定控件。

本主题描述可用于创建数据绑定控件的数据源。 它还描述了数据绑定中涉及的一些常规任务。 有关如何创建数据绑定控件的更具体的详细信息，请参阅[将 Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)，并[将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

## <a name="data-sources"></a>数据源

在数据绑定的上下文中，数据源表示内存中的数据，这些数据可以绑定到您的用户界面。 在实际情况下，数据源可以是实体框架类、数据集、封装在 .net 代理对象中的服务终结点、LINQ to SQL 类或任何 .net 对象或集合。 某些数据源支持通过从“数据源”窗口拖动项来创建数据绑定控件，而其他数据源则不能。 下表显示了支持的数据源。

| 数据源 | Windows 窗体设计器中的拖放支持 | WPF 设计器中的拖放支持 | Silverlight 设计器中的拖放支持 |
| - | - | - | - |
| 数据集 | 是 | 是 | 否 |
| 实体数据模型 | 是<sup>1</sup> | 是 | 是 |
| LINQ to SQL 类 | 否<sup>2</sup> | 否<sup>2</sup> | 否<sup>2</sup> |
| 服务（包括 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]、WCF 服务和 Web 服务） | 是 | 是 | 是 |
| 对象 | 是 | 是 | 是 |
| SharePoint | 是 | 是 | 是 |

1. 使用 **实体数据模型** 向导生成模型，然后将这些对象拖到设计器中。

2. LINQ to SQL 类不会出现在“数据源”窗口中。 不过，你可以添加基于 LINQ to SQL 类的新对象数据源，然后将这些对象拖到设计器来创建数据绑定控件。 有关详细信息，请参阅[演练：创建 LINQ to SQL 类 (O-R 设计器) ](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="data-sources-window"></a>“数据源”窗口

数据源以“数据源”窗口中的项的形式提供给项目。 当窗体设计图面是您的项目中的活动窗口时，或者您 (可以通过选择 "**查看**  >  **其他 Windows**  >  **数据源**") 打开项目时，将显示此窗口。 您可以从此窗口拖动项来创建绑定到基础数据的控件，还可以通过右键单击来配置数据源。

![“数据源”窗口](../data-tools/media/raddata-data-sources-window.png)

对于显示在“数据源”窗口中的每个数据类型，将该项拖到设计器时，都会创建一个默认控件。 在从 " **数据源** " 窗口中拖动项之前，可以更改创建的控件。 有关详细信息，请参阅 [设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="tasks-involved-in-binding-controls-to-data"></a>将控件绑定到数据所涉及的任务

下表列出了将控件绑定到数据时执行的一些最常见任务。

|任务|详细信息|
|----------| - |
|打开“数据源”窗口。|在编辑器中打开设计图面，然后选择 "**查看**  >  **数据源**"。|
|将数据源添加到项目中。|[添加新数据源](../data-tools/add-new-data-sources.md)|
|设置在将项从“数据源”窗口拖到设计器时创建的控件。|[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|修改与“数据源”窗口中的项关联的控件的列表。|[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|创建数据绑定控件。|[在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|绑定到对象或集合。|[Visual Studio 中的绑定对象](../data-tools/bind-objects-in-visual-studio.md)|
|筛选 UI 中显示的数据。|[在 Windows 窗体应用程序中对数据进行筛选和排序](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|自定义控件的标题。|[自定义 Visual Studio 创建数据绑定控件的标题的方式](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Windows窗体数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)
