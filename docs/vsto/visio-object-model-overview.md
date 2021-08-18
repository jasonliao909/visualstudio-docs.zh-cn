---
title: Visio 对象模型概述
description: 了解如何与 Visio 对象模型进行交互，以便为 Microsoft Visio 开发 Office 解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visio [Office development in Visual Studio], object model
- object models [Office development in Visual Studio], Office
- object models [Office development in Visual Studio], Visio
- objects [Office development in Visual Studio], Office object models
- Office object models
- Visio object model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: e2c82deca11d11d96afce5365b04b68247807789
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122046342"
---
# <a name="visio-object-model-overview"></a>Visio 对象模型概述
  要为 Microsoft Office Visio 开发 Office 解决方案，则可以与 Visio 对象模型进行交互。 此对象模型包含 Visio 中主互操作程序集所提供的类和接口，并在 `Microsoft.Office.Interop.Visio` 命名空间中定义。

 本主题概要介绍 Visio 对象模型。 有关使用 Visio 对象模型在 Office 项目中执行任务的信息，请参阅以下主题：

- [使用 Visio 文档](../vsto/working-with-visio-documents.md)

- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)

## <a name="understand-the-visio-object-model"></a>了解 Visio 对象模型
 Visio 提供了许多可与之交互的对象。 这些对象采用严格遵循用户界面的层次结构进行组织。 层次结构的顶部是 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application) 对象。 此对象表示 Visio 的当前实例。 `Microsoft.Office.Interop.Visio.Application`对象包含 `Microsoft.Office.Interop.Visio.Document` 和对象以及 `Microsoft.Office.Interop.Visio.Page` `Microsoft.Office.Interop.Visio.Documents` 和 `Microsoft.Office.Interop.Visio.Pages` 集合。 每个对象和集合都有许多方法和属性，可进行访问以便操作并与其进行交互。

 有关详细信息，请参阅适用于 [Microsoft.Office.Interop.Visio.Application](/office/vba/api/Visio.Application)、 [Microsoft.Office.Interop.Visio.Document](/office/vba/api/Visio.Document)和 [Microsoft.Office.Interop.Visio.Page](/office/vba/api/Visio.Page) 对象，以及 [Microsoft.Office.Interop.Visio.Documents](/office/vba/api/Visio.Documents) 和 [Microsoft.Office.Interop.Visio.Pages](/office/vba/api/Visio.Pages) 集合的 VBA 的参考文档。

 下列各节简要介绍了顶级对象以及它们彼此交互的方式。 这些对象包括以下对象：

- 应用程序对象

- 文档对象

- Page 对象

### <a name="application-object"></a>应用程序对象
 Microsoft。Office。交互.Visio。application 对象表示 Visio 应用程序，并且是所有其他对象的父级。 其成员通常作为一个整体应用于 Visio。 您可以使用 Microsoft 的属性和方法。Office。交互.Visio。`Microsoft.Office.Interop.Visio.ApplicationSettings`用于控制 Visio 环境的应用程序和对象。

 在 VSTO 外接程序项目中，可以访问 Microsoft。Office。交互.Visio。应用程序对象，方法是使用 `Application` 类的字段 `ThisAddIn` 。 有关更多信息，请参见 [Programming VSTO Add-Ins](../vsto/programming-vsto-add-ins.md)。

### <a name="document-object"></a>文档对象
 Microsoft.Office.Interop.Visio.Docargumentable 对象是对 Visio 编程的核心。 它表示绘图、模具或模板文件。 打开 Visio 文档或创建新文档时，将创建一个新的 Microsoft.Office.Interop.Visio.Docargumentable 对象，该对象将添加到 Microsoft 的 Microsoft.Office.Interop.Visio.Documents 集合中。Office。交互.Visio。应用程序对象。

 具有焦点的文档被称为活动文档。 它由 `Microsoft.Office.Interop.Visio.Application.ActiveDocument` Office 的属性表示。交互.Visio。应用程序对象。

### <a name="page-object"></a>Page 对象
 Microsoft。Office。交互.Visio。Page 对象表示前景页面或背景页的绘图区域。 可以使用 `Microsoft.Office.Interop.Visio.Page.Background` 属性来确定某页是前景页还是背景页。

 若要创建形状，则可以使用包含 `Microsoft.Office.Interop.Visio.Page.DrawSpline` 和 `Microsoft.Office.Interop.Visio.Page.DrawOval` 方法的方法。 此外，可以通过使用 `Microsoft.Office.Interop.Visio.Page.Drop` 或 `Microsoft.Office.Interop.Visio.Page.DropMany` 方法从模具检索母板，并将形状放置在页面上。

## <a name="use-the-visio-object-model-documentation"></a>使用 Visio 对象模型文档
 有关 Visio 对象模型的完整信息，可以参考 Visio VBA 对象模型引用。 VBA 对象模型引用在 Visio 对象模型被公开到 Visual Basic for Applications (VBA) 代码时记录该对象模型。 有关详细信息，请参阅[Visio 对象模型引用](/office/vba/api/overview/visio/object-model)。

 VBA 对象模型引用中的所有对象和成员都对应于 Visio 主互操作程序集 (PIA) 中的类型和成员。 例如， `Document` VBA 对象模型引用中的对象对应于 Visio PIA 中的 Microsoft.Office.Interop.Visio.Docargumentable 类型。 虽然 VBA 对象模型引用提供大多数属性、方法和事件的代码示例，但如果想要将其用于使用 Visual Studio 创建的 Visio VSTO 外接程序项目，则必须将本引用中的 VBA 代码转换成 Visual Basic 或 Visual C#。

> [!NOTE]
> 此时，没有任何 Visio 主互操作程序集的参考文档。

 有关相关的代码示例和用于创建 Visio 解决方案的其他工具，请参阅[Visio 2010 软件开发工具包](https://www.microsoft.com/download/details.aspx?id=12365)。

### <a name="additional-types-in-primary-interop-assemblies"></a>主互操作程序集中的其他类型
 可以在主互操作程序集中找到因为实现不同而对 VBA 不可见的类型。 VBA 提供 Visio 对象模型的视图，该视图仅包括可以直接使用的对象和成员。 主互操作程序集公开相同的对象模型，但它们还包括将 COM 对象模型中的对象转换为托管代码的其他接口、类和的成员。 这些附加项不应直接在代码中使用。

 有关详细信息，请参阅[Office 主互操作程序集中的类和接口概述](/previous-versions/office/office-12/ms247299(v=office.12))和[Office 主互操作程序集](../vsto/office-primary-interop-assemblies.md)。

## <a name="see-also"></a>请参阅
- [Visio 解决方案](../vsto/visio-solutions.md)
- [使用 Visio 文档](../vsto/working-with-visio-documents.md)
- [使用 Visio 形状](../vsto/working-with-visio-shapes.md)
