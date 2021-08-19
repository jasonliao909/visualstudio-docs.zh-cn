---
title: Visio 解决方案
description: 了解如何使用 VSTO 外接程序自动执行 Visio、扩展 Visio 功能，或 (UI) 自定义 Visio 用户界面。
ms.custom: SEO-VS-2020
ms.date: 08/14/2019
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], Visio
- solutions [Office development in Visual Studio], Visio
- Visio [Office development in Visual Studio]
- templates [Office development in Visual Studio], Visio
- projects [Office development in Visual Studio], Visio
- Office solutions [Office development in Visual Studio], Visio
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 14f3c77d35f0c2fea648897e091ac454dda5156b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046212"
---
# <a name="visio-solutions"></a>Visio 解决方案
  Visual Studio 提供可用于创建 Microsoft Office Visio 的 VSTO 外接程序的项目模板。 VSTO 外接程序可用于自动运行 Visio、扩展 Visio 功能或自定义 Visio 用户界面 (UI)。

 有关 VSTO 外接程序的详细信息，请参阅 VSTO 外接程序的[VSTO 外](../vsto/getting-started-programming-vsto-add-ins.md)接程序和[体系结构](../vsto/architecture-of-vsto-add-ins.md)。如果不熟悉如何与 Microsoft Office 进行编程，请参阅[Visual Studio&#41;中的 Office 开发入门 &#40;](../vsto/getting-started-office-development-in-visual-studio.md)。

 **适用于：** 本主题中的信息适用于 Visio 2010 的 VSTO 外接程序项目。 有关详细信息，请参阅[按 Office 应用程序和项目类型提供的功能](../vsto/features-available-by-office-application-and-project-type.md)。

[!include[Add-ins note](includes/addinsnote.md)]

## <a name="automate-visio-by-using-the-visio-object-model"></a>使用 Visio 对象模型自动 Visio
 Visio 对象模型公开了许多类，它们可用于自动运行 Visio 来创建针对组织结构图、流程图、项目时间线、网络图、办公区等关系图。 借助 API，你可以编写代码来完成常规任务：

- 在关系图中构造并放置形状和文本。

- 基于业务逻辑和用户输入管理形状行为。

- 控制关系图的可视化效果，如平移和缩放。

- 自定义应用程序 UI。

- 将外部数据导入 Visio，将其链接到形状并在页面上以图形方式显示。

  您可以查看有关使用 Visio 的对象模型处理文档和形状的分步过程和代码示例，以便处理[Visio 文档](../vsto/working-with-visio-documents.md)和[处理 Visio 形状](../vsto/working-with-visio-shapes.md)。

  若要从 VSTO 外接程序访问 Visio 对象模型，请使用项目中 `Application` 类的 `ThisAddIn` 字段。 `Application` 字段返回 `Microsoft.Office.Interop.Visio.Application` 对象，该对象表示 Visio 的当前实例。 有关详细信息，请参阅[Program VSTO 加载项](../vsto/programming-vsto-add-ins.md)。

  调入 Visio 对象模型时，将使用 Visio 的主互操作程序集 (PIA) 中提供的类型。 该 PIA 用作 VSTO 外接程序中的托管代码和 Visio 中的 COM 对象模型之间的桥梁。 Visio PIA 中的所有类型都在 `Microsoft.Office.Interop.Visio` 命名空间中进行定义。 有关主互操作程序集的详细信息，请参阅 VSTO&#41;和[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md) [Office 解决方案开发概述 &#40;](../vsto/office-solutions-development-overview-vsto.md) 。

## <a name="visio-object-model-overview"></a>Visio 对象模型概述
 可以在[Visio 对象模型概述](../vsto/visio-object-model-overview.md)中找到 Visio 对象模型的概述，其中包括指向 Visio 对象模型引用和 sdk 的链接。

## <a name="customize-the-user-interface-of-visio"></a>自定义 Visio 的用户界面
 该 Visio UI 还拥有以下自定义选项。

|任务|更多信息|
|----------|--------------------------|
|自定义功能区。|[功能区概述](../vsto/ribbon-overview.md)|

 有关自定义 Visio UI 的信息，请参阅 [Visio.UIObject](/office/vba/api/Visio.UIObject) 类的 VBA 参考文档。

## <a name="see-also"></a>请参阅
- [VSTO 外接程序编程入门](../vsto/getting-started-programming-vsto-add-ins.md)
- [Office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)
- [OfficeUI 自定义](../vsto/office-ui-customization.md)
- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)
- [Office 开发中的 Visio 2010](/previous-versions/office/developer/office-2010/ff604964(v=office.14))
