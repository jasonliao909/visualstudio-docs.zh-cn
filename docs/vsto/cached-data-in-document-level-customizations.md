---
title: 文档级自定义项中的缓存数据
description: 了解如何Visual Studio将数据嵌入为数据缓存，从而在文档级自定义项中将数据与视图分离。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data islands [Office development in Visual Studio]
- view [Office development in Visual Studio]
- caching data [Office development in Visual Studio], about caching data
- data caching [Office development in Visual Studio], about data caching
- data [Office development in Visual Studio], cache
- data [Office development in Visual Studio], document-level solutions
- document-level customizations [Office development in Visual Studio], data model
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 528e452142bbac81654a6f55878265ee544ddb39
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122083728"
---
# <a name="cached-data-in-document-level-customizations"></a>文档级自定义项中的缓存数据
  文档级自定义项的一个主要目标是将数据与文档中的视图Office分离。 数据是指文档中存储的信息，包括数字和文本。 视图是指 Word 和 Microsoft Office Excel 的用户界面Microsoft Office对象Microsoft Office Excel。

 Visual Studio将数据嵌入为数据岛（也称为数据缓存）来将数据与文档级自定义项 *中的视图分离*。  可以直接读取或修改数据，而无需启动 Word 或 Excel。 当需要修改未安装任何数据库的服务器上文档中Microsoft Office很有用。 Word 和 Excel旨在用于客户端环境;它们并非设计为在服务器上运行。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有关文档级自定义项的更多信息，请参阅 Office 解决方案开发概述[&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)和[文档级自定义的体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="understand-the-cached-data-programming-model"></a>了解缓存的数据编程模型
 数据岛可以包含解决方案中满足特定要求的任何对象。 这些对象包括 对象、对象以及可通过 类 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 序列化的其他任何 <xref:System.Xml.Serialization.XmlSerializer> 对象。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

 若要提供缓存数据的视图，可以将Windows窗体控件和宿主控件绑定到数据岛中的对象。  数据岛和数据绑定控件之间的数据绑定使两者保持同步。 还可以将验证代码添加到独立于控件的数据。 有关详细信息，请参阅将数据绑定到解决方案 中的[Office控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

 宿主控件是对象模型和 Word 对象模型中Excel对象的扩展版本。 与本机对象不同，宿主控件可以直接绑定到托管数据对象。 有关详细信息，请参阅主机[项和宿主控件概述Windows](../vsto/host-items-and-host-controls-overview.md)[窗体控件Office文档概述](../vsto/windows-forms-controls-on-office-documents-overview.md)。

## <a name="access-cached-data-on-the-server"></a>访问服务器上缓存的数据
 若要访问文档中的缓存数据，可以使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 类。 此类是 的一部分，可以在服务器上使用，而无需运行 Excel [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] Word。 当用户在修改缓存数据后打开文档时，绑定到数据的任何控件将自动同步到更改，并且向用户显示更新后的数据。 有关详细信息，请参阅 [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

 Excel和 Word 不需要写入到服务器上的数据，只需在客户端上查看数据。 Excel和 Word 甚至不需要安装在服务器上。 这提高了可伸缩性，并提供了对包含数据岛的文档执行快速批处理的能力。

## <a name="data-caching-for-offline-use"></a>脱机使用的数据缓存
 将数据存储在数据岛中可实现脱机方案。 当用户首次打开文档或从服务器请求文档时，数据岛将填充最新数据。 数据岛缓存在文档中，然后脱机可用。 即使 (实时连接) ，用户和代码库也可以操作数据。 当用户重新连接时，可以将对数据所做的更改传播回服务器数据源。

## <a name="cached-data-and-custom-xml-parts-compared"></a>缓存数据和自定义 XML 部件比较
 自定义 XML 部件是在 2007 Microsoft Office中引入的，用于将任意 XML 部分存储在文档中。 尽管自定义 XML 部件在许多与数据缓存相同的方案中很有用，但数据岛和自定义 XML 部件之间存在一些差异。 有关自定义 XML 部件的信息，请参阅 [自定义 XML 部件概述](../vsto/custom-xml-parts-overview.md)。

 下表列出了一些差异和相似之处。

|问题/特征|数据缓存|自定义 XML 部件|
|-|----------------|----------------------|
|哪些Office应用程序可以使用它们？|以下应用程序的文档级自定义：<br /><br /> - Excel<br />- Word|以下应用程序的文档级和应用程序级解决方案：<br /><br /> - Excel<br />- PowerPoint<br />- Word|
|可以存储哪些类型的数据？|自定义程序集中满足特定要求的任何公共对象。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。|任何 XML 数据。|
|能否在不启动应用程序的情况下Microsoft Office数据？|是，通过使用 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 提供的 类 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 。|是，通过使用 命名空间中的 <xref:System.IO.Packaging> 类，或者通过使用 Open XML Format SDK。|

## <a name="see-also"></a>请参阅
- [解决方案Office数据](../vsto/data-in-office-solutions.md)
- [Office 解决方案体系结构Visual Studio](../vsto/architecture-of-office-solutions-in-visual-studio.md)
