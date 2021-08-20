---
title: XMLNode 控件
description: 了解 XMLNode 控件是一个映射的 XML 节点对象，该对象公开事件并可绑定到数据。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 8b3c67526ac00f9cc7266f6bb93992505d3b70ad
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122068270"
---
# <a name="xmlnode-control"></a>XMLNode 控件
  **重要提示** 本主题中的关于 Microsoft Word 的信息是专门针对美国及其区域以外的个人和组织的权益和使用的，或者开发在上运行的程序 Microsoft Word （在2010年1月之前，microsoft 从 Microsoft Word 中的自定义 XML 删除了特定功能的实现。 对于在2010年1月10日之后使用、或开发 Microsoft Word 的程序 Microsoft Word 产品的美国或其所在区域中的个人或组织，可能无法读取或使用与有关的信息。对于该日期之前许可的产品，这些产品的行为并不相同，也不会在美国之外购买和许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNode>控件是一个用于公开事件并且可以绑定到数据的映射 XML 节点对象。 <xref:Microsoft.Office.Tools.Word.XMLNode>仅当非重复架构元素映射到 Microsoft Office Word 文档中时，才创建控件。 Visual Studio 创建 XML 节点后，可以直接对其进行编程，而无需遍历 Word 对象模型。

 <xref:Microsoft.Office.Tools.Word.XMLNode>只能通过删除 Word 中的元素映射来删除控件。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 <xref:Microsoft.Office.Tools.Word.XMLNode>控件支持简单数据绑定。 XML 节点应使用属性绑定到数据源 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 。 如果更新绑定数据集内的数据，则 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件会反映所做的更改。

## <a name="formatting"></a>格式设置
 可应用于对象的格式设置 <xref:Microsoft.Office.Interop.Word.XMLNode> 可应用于 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 其中包括字体、下划线样式和字符样式。

## <a name="events"></a>事件
 以下事件可用于 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件：

- <xref:Microsoft.Office.Tools.Word.XMLNode.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNode.BindingContextChanged>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNode.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNode.ValidationError>

## <a name="compare-events"></a>比较事件
 当用户将其光标移到特定控件的上下文中时，可以捕获事件 <xref:Microsoft.Office.Tools.Word.XMLNode> 。 例如，你可能有一个 <xref:Microsoft.Office.Tools.Word.XMLNode> 名为 `Customer` 的控件，该控件有一个 <xref:Microsoft.Office.Tools.Word.XMLNode> 名为的子控件 `Company` ，并 `Company` 有两个 <xref:Microsoft.Office.Tools.Word.XMLNode> 名为的子控件， `CompanyName` `CompanyRegion` 如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果您想要在每次将光标移到节点时在 "操作" 窗格上显示一个控件，是将 `Company` 游标置于 `CompanyName` 还是的上下文中是不重要的 `CompanyRegion` `Company` 。 在这种情况下，你可以在的事件中编写代码 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `Company` 。

 在大多数情况下，当光标进入 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件时，将 <xref:Microsoft.Office.Tools.Word.XMLNode.Select> 引发和 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> 事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|将光标置于内时发生 <xref:Microsoft.Office.Tools.Word.XMLNode> 。|当光标从 <xref:Microsoft.Office.Tools.Word.XMLNode> 节点的上下文外的区域移入该节点或它的一个子节点内时发生此事件。 换言之，仅当上下文发生更改时才会引发。|

 例如，当你将光标从外移到时 `Customer` `CompanyName` ，将 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `Customer` 引发、和的事件 `Company` `CompanyName` 。 如果然后将光标从移 `CompanyName` 到 `CompanyRegion` ，则只引发的 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> 事件， `CompanyRegion` 因为你仍在和的上下文中 `Company` `Customer` 。

 事件与事件之间的差异相同 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave> <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect> 。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNodes 控件](../vsto/xmlnodes-control.md)
- [如何：将 XMLNode 控件添加到 Word 文档](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [如何：将架构映射到 Visual Studio 中的 Word 文档](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [宿主项和宿主控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
