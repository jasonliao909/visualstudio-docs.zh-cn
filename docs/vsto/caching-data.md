---
title: 缓存数据
description: 了解如何在文档级自定义项中缓存数据对象，以便脱机或不打开 Word 或 Microsoft Office访问Excel。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data caching [Office development in Visual Studio], about caching data
- data [Office development in Visual Studio], caching
- data caching [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: f8779089fc4987d600f3860151782d0322f9d1fd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602526"
---
# <a name="cache-data"></a>缓存数据
  可以在文档级自定义项中缓存数据对象，以便可以脱机访问数据，或者无需打开 Word 或 Microsoft Office Microsoft Office Excel。 若要缓存对象，对象必须具有满足特定要求的数据类型。 中的许多常见数据类型.NET Framework这些要求，包括 <xref:System.String> <xref:System.Data.DataSet> 、 和 <xref:System.Data.DataTable> 。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 有两种方法可以将对象添加到数据缓存：

- 若要在生成解决方案时将对象添加到数据缓存，请对对象 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 声明应用 属性。 有关详细信息，请参阅 [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)。

- 若要以编程方式运行时向数据缓存添加对象，请使用主机项的 方法， `StartCaching` 如 `ThisDocument` 或 `ThisWorkbook` 类。 有关详细信息，请参阅[如何：以](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)编程方式将数据源缓存在Office文档中。

  将对象添加到数据缓存后，无需启动 Word 或 Excel 即可访问和修改缓存Excel。 有关详细信息，请参阅 [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="requirements-for-data-objects-to-be-cached"></a>要缓存的数据对象的要求
 若要在解决方案中缓存数据对象，该对象必须满足以下要求：

- 是宿主项（如 或 类）的读/写公共字段 `ThisDocument` 或 `ThisWorkbook` 属性。

- 不是索引器或其他参数化属性。

  此外，数据对象必须由 类序列化，这意味着该对象 <xref:System.Xml.Serialization.XmlSerializer> 的类型必须具有以下特征：

- 是公共类型。

- 具有没有参数的公共构造函数。

- 不执行需要其他安全特权的代码。

- 仅公开读/写公共 (将忽略其他属性) 。

- 不公开多维数组 (接受嵌套数组) 。

- 不从属性和字段返回接口。

- 如果集合 <xref:System.Collections.IDictionary> ，不实现 。

  缓存数据对象时， 将对象序列化为存储在文档中自定义 XML 部件 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] *中的 XML* 字符串。 有关详细信息，请参阅自定义 [XML 部件概述](../vsto/custom-xml-parts-overview.md)。

## <a name="cached-data-size-limits"></a>缓存的数据大小限制
 可以添加到文档中的数据缓存的数据总量和数据缓存中任何单个对象的大小存在一些限制。 如果超过这些限制，则当数据保存到数据缓存时，应用程序可能会意外关闭。

 若要避免这些限制，请遵循以下准则：

- 不要向数据缓存添加任何大于 10 MB 的对象。

- 不要将超过 100 MB 的总数据添加到单个文档中的数据缓存。

  这些是近似值。 确切的限制取决于多种因素，包括可用 RAM 和正在运行的进程数。

## <a name="control-the-behavior-of-cached-objects"></a>控制缓存对象的行为
 若要进一步控制缓存对象的行为，可以在缓存对象的类型上 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> 实现 接口。 例如，如果要控制更改对象时通知用户的方法，可以实现此接口。 有关演示如何实现 的代码示例，请参阅 Excel 开发示例和演练中的 Excel 动态控件示例和 Word 动态控件Office中的 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.ICachedType> `ControlCollection` [类](../vsto/office-development-samples-and-walkthroughs.md)。

## <a name="persist-changes-to-cached-data-in-password-protected-documents"></a>在受密码保护的文档中保留对缓存数据所做的更改
 如果在受密码保护的文档中缓存数据对象，则不会保存对缓存数据所做的更改。 可以通过重写两种方法来保存对缓存数据所做的更改。 重写这些方法以在保存文档时暂时删除保护，然后在保存操作完成后重新应用保护。

 有关详细信息，请参阅如何：在受密码保护的文档 [中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)。

## <a name="prevent-data-loss-when-adding-null-values-to-the-data-cache"></a>在向数据缓存添加 null 值时防止数据丢失
 将对象添加到数据缓存时，必须先将所有缓存对象初始化为非 **null** 值，然后才能保存和关闭文档。 如果保存和关闭 **文档** 时，任何缓存对象都有 null 值，则 将自动从数据缓存中删除 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 所有缓存对象。

 如果在设计时使用 属性将值为 **null** 的对象添加到数据缓存，则您可以使用 类在打开文档之前初始化缓存 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 的数据对象。 如果要在最终用户打开文档之前，在未安装 Word 或 Excel在服务器上初始化缓存的数据，这非常有用。 有关详细信息，请参阅 [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)。

## <a name="see-also"></a>另请参阅
- [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：以编程方式将数据源缓存在Office文档中](../vsto/how-to-programmatically-cache-a-data-source-in-an-office-document.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [演练：使用缓存数据集创建主详细信息关系](../vsto/walkthrough-creating-a-master-detail-relation-using-a-cached-dataset.md)
