---
title: XMLNode 控件
description: 了解 XMLNode 控件是一个映射的 XML 节点对象，该对象公开事件并可以绑定到数据。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664918"
---
# <a name="xmlnode-control"></a>XMLNode 控件
  **重要** 本主题中针对 Microsoft Word 设置的信息专门供位于 美国 及其区域之外的个人和组织使用，或者使用或开发在 2010 年 1 月之前由 Microsoft 许可的 Microsoft Word 产品（当 Microsoft 从 Microsoft Word 中删除与自定义 XML 相关的特定功能的实现时）运行的程序。 有关 Microsoft Word 的信息不能由 美国 或其区域使用或开发在 2010 年 1 月 10 日之后由 Microsoft 许可的 Microsoft Word 产品运行的程序的个人或组织读取或使用;这些产品的行为与该日期之前许可的产品或购买和许可用于外部产品美国。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNode>控件是一个映射的 XML 节点对象，该对象公开事件并可以绑定到数据。 只有在将非重复架构元素映射到 Word 文档中时 <xref:Microsoft.Office.Tools.Word.XMLNode> ，Microsoft Office控件。 创建Visual Studio XML 节点后，可以直接针对它进行编程，而无需遍历 Word 对象模型。

 <xref:Microsoft.Office.Tools.Word.XMLNode>控件只能删除 Word 中的元素映射。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 控件 <xref:Microsoft.Office.Tools.Word.XMLNode> 支持简单数据绑定。 XML 节点应通过使用 属性绑定到 <xref:System.Windows.Forms.IBindableComponent.DataBindings%2A> 数据源。 如果更新绑定数据集内的数据，则 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件会反映所做的更改。

## <a name="formatting"></a>格式化
 可应用于 对象的格式 <xref:Microsoft.Office.Interop.Word.XMLNode> 设置可以应用于 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 这包括字体、下划线样式和字符样式。

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
 当用户将光标移到特定控件的上下文中时，可以捕获 <xref:Microsoft.Office.Tools.Word.XMLNode> 事件。 例如，你可能有一个名为 的控件，该控件具有名为 的子控件，并且有两个名为 和 的子 <xref:Microsoft.Office.Tools.Word.XMLNode> `Customer` <xref:Microsoft.Office.Tools.Word.XMLNode> `Company` `Company` <xref:Microsoft.Office.Tools.Word.XMLNode> `CompanyName` `CompanyRegion` 控件，如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果希望在将光标移动到节点时在操作窗格上显示控件，则光标是放置在 中还是都位于 的上下文中并不重要 `Company` `CompanyName` `CompanyRegion` `Company` 。 在这种情况下，可以在 的 事件中 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> 编写代码 `Company` 。

 在大多数情况下，当光标进入控件 <xref:Microsoft.Office.Tools.Word.XMLNode> 时，将同时引发 <xref:Microsoft.Office.Tools.Word.XMLNode.Select> 和 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> 事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|当光标置于 内时发生 <xref:Microsoft.Office.Tools.Word.XMLNode> 。|当光标从 <xref:Microsoft.Office.Tools.Word.XMLNode> 节点的上下文外的区域移入该节点或它的一个子节点内时发生此事件。 换句话说，仅在上下文更改时引发它。|

 例如，将光标从 外部移动到 时，将引发 、 和 `Customer` `CompanyName` 的 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `Customer` `Company` `CompanyName` 事件。 如果随后将光标从 移动到 ，则只引发 的 事件，因为你仍在 和 `CompanyName` `CompanyRegion` <xref:Microsoft.Office.Tools.Word.XMLNode.ContextEnter> `CompanyRegion` 的 `Company` 上下文中 `Customer` 。

 事件和 事件之间存在 <xref:Microsoft.Office.Tools.Word.XMLNode.ContextLeave> 相同的 <xref:Microsoft.Office.Tools.Word.XMLNode.Deselect> 差异。

## <a name="see-also"></a>另请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNodes 控件](../vsto/xmlnodes-control.md)
- [如何：将 XMLNode 控件添加到 Word 文档](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)
- [如何：将架构映射到文档中的 Word Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
