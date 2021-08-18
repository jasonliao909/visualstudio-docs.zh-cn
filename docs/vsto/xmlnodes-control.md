---
title: XMLNodes 控件
description: 了解 XMLNodes 控件仅在重复架构元素映射到文档时Microsoft Word创建。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNodes control, events
- XMLNodes control
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: cad5ca717f5e996fcc32c4806c6ab86afc7cc241
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122045900"
---
# <a name="xmlnodes-control"></a>XMLNodes 控件
  **重要** 本主题中介绍的关于 Microsoft Word 的信息专门供位于 美国 及其区域之外的个人和组织受益和使用，或者使用或开发在 2010 年 1 月之前由 Microsoft 许可的 Microsoft Word 产品（在 Microsoft Word 中实现与自定义 XML 相关的特定功能）的程序。 有关 Microsoft Word 的信息不能由 美国 或其区域使用或开发在 2010 年 1 月 10 日之后由 Microsoft 许可的 Microsoft Word 产品运行的程序的个人或组织读取或使用;这些产品的行为与该日期之前许可的产品或购买和许可在产品外部使用的产品美国。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 <xref:Microsoft.Office.Tools.Word.XMLNodes>控件是公开事件的映射 XML 节点对象的集合。 只有在重复的架构元素映射到 Word 文档中时，Microsoft Office <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件。 如果重复元素包含子元素，则每个子元素也将创建为 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件。

 创建Visual Studio XML 节点的集合后，可以直接针对 控件进行编程，而无需遍历 Word 对象模型。 <xref:Microsoft.Office.Tools.Word.XMLNodes>只有从文档中删除元素映射，才能删除该控件。

> [!NOTE]
> 如果通过 属性访问 控件的子 <xref:Microsoft.Office.Tools.Word.XMLNodes> <xref:Microsoft.Office.Tools.Word.XMLNodes.Item%2A> 元素，它将返回 <xref:Microsoft.Office.Interop.Word.XMLNode> 对象而不是 <xref:Microsoft.Office.Tools.Word.XMLNode> 控件。 有关详细信息，请参阅主机 [项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)。

## <a name="bind-data-to-the-control"></a>将数据绑定到控件
 控件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 不支持数据绑定。 这是因为控件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 没有复杂的数据绑定功能，并且简单数据绑定不能表示重复数据。

## <a name="formatting"></a>格式设置
 可应用于文档中文本的任何格式设置都可以应用于 <xref:Microsoft.Office.Tools.Word.XMLNodes> 控件。

## <a name="events"></a>事件
 可用于 控件的事件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 包括：

- <xref:Microsoft.Office.Tools.Word.XMLNodes.AfterInsert>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.BeforeDelete>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect>

- <xref:System.ComponentModel.IComponent.Disposed>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.Select>

- <xref:Microsoft.Office.Tools.Word.XMLNodes.ValidationError>

## <a name="compare-events"></a>比较事件
 当用户将光标移到特定控件的上下文中时，可以捕获 <xref:Microsoft.Office.Tools.Word.XMLNodes> 事件。 例如，你可能有一个名为 的控件，该控件具有名为 的子控件，并且有两个名为 和 的子 <xref:Microsoft.Office.Tools.Word.XMLNodes> `Customer` <xref:Microsoft.Office.Tools.Word.XMLNodes> `Company` `Company` <xref:Microsoft.Office.Tools.Word.XMLNodes> `CompanyName` `CompanyRegion` 控件，如下所示：

```xml
<Customer>
    <Company>
        <CompanyName>
        <CompanyRegion>
```

 如果希望在将光标移动到节点时在操作窗格上显示控件，则光标是放置在 中还是都位于 的上下文中并不重要 `Company` `CompanyName` `CompanyRegion` `Company` 。 在这种情况下，可以在 的 事件中 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> 编写代码 `Company` 。

 在大多数情况下，当光标进入控件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 时，将同时引发 <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> 和 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> 事件。 下表显示了这些事件之间的差异。

|选择事件|ContextEnter 事件|
|------------------|------------------------|
|当光标放置在 <xref:Microsoft.Office.Tools.Word.XMLNodes> 集合的一个节点中时发生此事件。|当光标从节点上下文以外的区域移入 <xref:Microsoft.Office.Tools.Word.XMLNodes> 集合的节点或子代节点之一时发生。 换句话说，它仅在上下文更改时引发，并且可以针对多个嵌套控件 <xref:Microsoft.Office.Tools.Word.XMLNodes> 引发。|

 例如，将光标从 外部移动到 时，将引发 、 和 `Customer` `CompanyName` <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> `Customer` `Company` `CompanyName` 的事件。 如果随后将光标从 移动到 ，则只引发 的 事件，因为 和 的上下文 `CompanyName` `CompanyRegion` <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextEnter> `CompanyRegion` `Company` 是相同的 `Customer` 。 文档中可以 `Company` 有多个节点。 如果将光标从一个 的节点移到另一个 的节点，则上下文是相同的， `CompanyName` `Company` `CompanyName` `Company` 因此只 <xref:Microsoft.Office.Tools.Word.XMLNodes.Select> 引发 事件。

 事件和 事件之间存在 <xref:Microsoft.Office.Tools.Word.XMLNodes.ContextLeave> 相同的 <xref:Microsoft.Office.Tools.Word.XMLNodes.Deselect> 差异。

## <a name="see-also"></a>请参阅
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [使用扩展对象自动执行 Word](../vsto/automating-word-by-using-extended-objects.md)
- [XMLNode 控件](../vsto/xmlnode-control.md)
- [如何：将 XMLNodes 控件添加到 Word 文档](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)
- [如何：将架构映射到文档中的 Word Visual Studio](../vsto/how-to-map-schemas-to-word-documents-inside-visual-studio.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
