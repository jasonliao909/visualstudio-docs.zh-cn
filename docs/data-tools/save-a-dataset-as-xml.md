---
title: 将数据集另存为 XML
description: 将数据集另存为 XML。 通过调用数据集上的可用 XML 方法（如 GetXml 或 WriteXml）来访问数据集中的 XML 数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML [Visual Basic], datasets
- data [Visual Studio], saving as XML
- datasets [Visual Basic], saving as XML
- saving data
ms.assetid: 68b8327c-ae05-49ff-b9ba-99183e70b52c
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 127e97c92d9b331fe3cc461c585fb3240482fbd0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601112"
---
# <a name="save-a-dataset-as-xml"></a>将数据集另存为 XML

通过调用数据集上的可用 XML 方法来访问数据集中的 XML 数据。 若要以 XML 格式保存数据，可以调用 <xref:System.Data.DataSet> 的 <xref:System.Data.DataSet.GetXml%2A> 方法和 <xref:System.Data.DataSet.WriteXml%2A> 方法。

调用 <xref:System.Data.DataSet.GetXml%2A> 方法将返回一个字符串，该字符串包含数据集中所有格式为 XML 的数据表中的数据。

调用 <xref:System.Data.DataSet.WriteXml%2A> 方法会将 XML 格式的数据发送到你指定的文件。

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-variable"></a>将数据集中的数据以 XML 形式保存到变量

- <xref:System.Data.DataSet.GetXml%2A> 方法返回 <xref:System.String>。 声明类型 <xref:System.String> 的变量，并为其分配 <xref:System.Data.DataSet.GetXml%2A> 方法的结果。

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet12":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet12":::

## <a name="to-save-the-data-in-a-dataset-as-xml-to-a-file"></a>将数据集中的数据以 XML 形式保存到文件

- <xref:System.Data.DataSet.WriteXml%2A> 方法有多个重载。 声明一个变量，并为其分配用于保存文件的有效路径。 下面的代码演示如何将数据保存到文件：

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb" id="Snippet13":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs" id="Snippet13":::

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
