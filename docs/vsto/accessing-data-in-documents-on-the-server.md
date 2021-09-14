---
title: 访问服务器上文档中的数据
description: 了解如何针对文档级自定义项中的数据进行编程，而无需使用 Word 或 Microsoft Office 对象Microsoft Office Excel。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], accessing on server
- data access [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: 21723deada493dd5e3d6ab6a16c6dc6366829bbb
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664772"
---
# <a name="access-data-in-documents-on-the-server"></a>访问服务器上文档中的数据
  可以针对文档级自定义项中的数据进行编程，而无需使用 Word 或 Microsoft Office 对象Microsoft Office Excel。 这意味着可以访问未安装 Word 或 Excel服务器的文档中包含的数据。 例如，服务器上的代码 (例如，在页) 可以自定义文档中的数据并将自定义的文档 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 发送给最终用户。 当最终用户打开文档时，解决方案程序集中的数据绑定代码将自定义数据绑定到文档中。 这是可能的，因为文档中的数据与用户界面分离。 有关详细信息，请参阅 [文档级自定义项 中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

## <a name="cache-data-for-use-on-a-server"></a>缓存数据以在服务器上使用
 若要在文档中缓存数据对象，在设计时请使用 属性将其标记为 ，或使用运行时宿主 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> `StartCaching` 项的 方法。 在文档中缓存数据对象时， 将该对象序列化为存储在文档中 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 的 XML 字符串。 对象必须满足某些要求才能进行缓存。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

 服务器端代码可以操作数据缓存中的任何数据对象。 绑定到缓存数据实例的控件与用户界面同步，因此，在客户端上打开文档时，对数据进行的任何服务器端更改都会自动显示。

## <a name="access-data-in-the-cache"></a>访问缓存中的数据
 可以从应用程序外部的应用程序访问缓存Office例如，从控制台应用程序、Windows窗体应用程序或网页。 访问缓存数据的应用程序必须具有完全信任;具有部分信任的 Web 应用程序无法插入、检索或更改缓存在文档Office数据。

 数据缓存可通过 集合的层次结构访问，集合由 类的 属性 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 公开：

- <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A>属性返回 <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> ，它包含文档级自定义项中所有缓存的数据。

- 每个 <xref:Microsoft.VisualStudio.Tools.Applications.CachedData> 均包含一个或多个 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> 对象。 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem>包含单个类中定义的所有缓存数据对象。

- 每个 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataHostItem> 均包含一个或多个 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 对象。 表示 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> 单个缓存的数据对象。

  下面的代码示例演示如何访问工作簿项目的 类中的缓存 `Sheet1` Excel字符串。 此示例是为 方法提供的较大示例的一 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> 部分。

  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs" id="Snippet12":::
  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb" id="Snippet12":::

## <a name="modify-data-in-the-cache"></a>修改缓存中的数据
 若要修改缓存的数据对象，通常请执行以下步骤：

1. 将缓存对象的 XML 表示形式反初始化为 对象的新实例。 可以使用表示缓存数据对象的 的 属性来访问 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem> XML。

2. 对此副本进行更改。

3. 使用下列选项之一将已更改的对象序列化回数据缓存：

    - 如果要自动序列化更改，请使用 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> 方法。 此方法使用 **DiffGram** 格式序列化数据缓存中的 、 和 <xref:System.Data.DataSet> <xref:System.Data.DataTable> 类型化数据集对象。 **DiffGram** 格式可确保脱机文档中对数据缓存的更改正确发送到服务器。

    - 如果要对缓存数据的更改执行自己的序列化，可以直接写入 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.Xml%2A> 属性。 如果使用 **通过更改** 、 或类型数据集中的数据来更新数据库，请指定 DiffGram <xref:System.Data.Common.DataAdapter> <xref:System.Data.DataSet> <xref:System.Data.DataTable> 格式。 否则， <xref:System.Data.Common.DataAdapter> 会通过添加新行而不是修改现有行来更新数据库。

### <a name="modify-data-without-deserializing-the-current-value"></a>修改数据而不反初始化当前值
 在某些情况下，你可能想要修改缓存对象的值，而无需先反化当前值。 例如，如果要更改具有简单类型（如字符串或整数）的对象的值，或者正在初始化服务器上文档中缓存的 ，可以这样做 <xref:System.Data.DataSet> 。 在这些情况下，可以使用 方法，而无需先反化缓存对象的 <xref:Microsoft.VisualStudio.Tools.Applications.CachedDataItem.SerializeDataInstance%2A> 当前值。

 下面的代码示例演示如何在工作簿项目的 类中更改缓存Excel `Sheet1` 的值。 此示例是为 方法提供的较大示例的一 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.Save%2A> 部分。

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ServerDocument/Form1.cs" id="Snippet11":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ServerDocument/Form1.vb" id="Snippet11":::

### <a name="modify-null-values-in-the-data-cache"></a>修改数据缓存中的 null 值
 保存和关闭文档时，数据缓存不会存储值为 **null** 的对象。 修改缓存数据时，此限制会产生多个后果：

- 如果将数据缓存中的任意对象设置为 **null** 值，则打开文档时，数据缓存中所有对象将自动设置为 **null，** 并且保存和关闭文档时将清除整个数据缓存。 也就是说，将从数据缓存中删除所有缓存对象，并且 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument.CachedData%2A> 集合将为空。

- 如果在数据缓存中生成具有 **null** 对象的解决方案，并且想要在首次打开文档之前使用 类初始化这些对象，则必须确保初始化数据缓存中所有 <xref:Microsoft.VisualStudio.Tools.Applications.ServerDocument> 对象。 如果只初始化某些 对象，则打开文档时，所有对象都将设置为 **null，** 并且保存和关闭文档时将清除整个数据缓存。

## <a name="access-typed-datasets-in-the-cache"></a>访问缓存中的类型数据集
 如果要从 Office 解决方案和 Office 外部的应用程序（例如 Windows Forms 应用程序或项目）访问类型数据集中的数据，则必须在两个项目引用的单独程序集中定义类型数据集。 [!INCLUDE[vstecasp](../sharepoint/includes/vstecasp-md.md)] 如果使用数据源配置向导或 **数据集设计器** 将类型数据集添加到每个项目，则 .NET Framework 将两个项目中的类型数据集视为不同的类型。 有关创建类型数据集的信息，请参阅在 中创建和配置[Visual Studio。](../data-tools/create-and-configure-datasets-in-visual-studio.md)

## <a name="see-also"></a>另请参阅

- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [文档级自定义项中的缓存数据](../vsto/cached-data-in-document-level-customizations.md)