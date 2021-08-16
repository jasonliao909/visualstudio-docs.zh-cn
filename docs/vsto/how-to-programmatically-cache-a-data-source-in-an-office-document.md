---
title: 以编程方式在Office缓存数据源
description: 了解如何通过调用宿主项的 StartCaching 方法，以编程方式将数据对象添加到文档中的数据缓存。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office applications [Office development in Visual Studio], data
- datasets [Office development in Visual Studio], caching
- StartCaching method
- data caching [Office development in Visual Studio], programmatically
- data [Office development in Visual Studio], caching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.technology: office-development
ms.workload:
- office
ms.openlocfilehash: eeede798542499d6a482b1a42b626e73170d024e864ec941c66e72a1b131bba3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121408768"
---
# <a name="how-to-programmatically-cache-a-data-source-in-an-office-document"></a>如何：以编程方式将数据源缓存在Office文档中
  可以通过调用宿主项（如 、 或 ）的 方法，以编程方式将数据对象添加到 `StartCaching` <xref:Microsoft.Office.Tools.Word.Document> 文档中的数据 <xref:Microsoft.Office.Tools.Excel.Workbook> 缓存 <xref:Microsoft.Office.Tools.Excel.Worksheet> 。 通过调用宿主项的 方法，从数据缓存 `StopCaching` 中删除数据对象。

 `StartCaching`方法和 方法都是 `StopCaching` 私有的，但它们显示在 IntelliSense 中。

 [!INCLUDE[appliesto_alldoc](../vsto/includes/appliesto-alldoc-md.md)]

 使用 方法将数据对象添加到数据缓存时，不需要使用 属性 `StartCaching` 声明数据 <xref:Microsoft.VisualStudio.Tools.Applications.Runtime.CachedAttribute> 对象。 但是，数据对象必须满足要添加到数据缓存的某些要求。 有关详细信息，请参阅缓存 [数据](../vsto/caching-data.md)。

## <a name="to-programmatically-cache-a-data-object"></a>以编程方式缓存数据对象

1. 在类级别（而不是方法内部）声明数据对象。 此示例假设要声明要以 <xref:System.Data.DataSet> `dataSet1` 编程方式缓存的名为 的 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet12":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet12":::

2. 实例化数据对象，然后调用文档或工作表实例的 方法并 `StartCaching` 传递数据对象的名称。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet13":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet13":::

## <a name="to-stop-caching-a-data-object"></a>停止缓存数据对象

1. 调用 `StopCaching` 文档或工作表实例的 方法，并传递数据对象的名称。 此示例假定你有一个 <xref:System.Data.DataSet> 要 `dataSet1` 停止缓存的名为 的 。

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb" id="Snippet14":::

    > [!NOTE]
    > 对于文档 `StopCaching` 或工作表的事件，请勿从 `Shutdown` 事件处理程序调用 。 引发事件时， `Shutdown` 修改数据缓存为时已晚。 有关 事件详细信息 `Shutdown` ，请参阅 Office[中的事件](../vsto/events-in-office-projects.md)。

## <a name="see-also"></a>请参阅

- [缓存数据](../vsto/caching-data.md)
- [如何：缓存数据以脱机或在服务器上使用](../vsto/how-to-cache-data-for-use-offline-or-on-a-server.md)
- [如何：在受密码保护的文档中缓存数据](../vsto/how-to-cache-data-in-a-password-protected-document.md)
- [访问服务器上文档中的数据](../vsto/accessing-data-in-documents-on-the-server.md)
- [保存数据](../data-tools/save-data-back-to-the-database.md)
