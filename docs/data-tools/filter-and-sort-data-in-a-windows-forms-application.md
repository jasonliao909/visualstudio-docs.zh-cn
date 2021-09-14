---
title: 在 Windows 窗体应用程序中对数据进行筛选和排序
description: 在 Windows 窗体应用程序中对数据进行筛选和排序。 将 "筛选器" 属性设置为一个字符串表达式，该表达式返回所需的记录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- row states, filtering
- data views, sorting
- row version, filtering
- row states
- data views, filtering
- sorting datasets, using data views
- dataset filtering, using data views
ms.assetid: f4f100f1-776d-46dc-b2fd-5b35b98d9561
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 0743bea71f972b5f5baa6909300c2ce669fc30a6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601157"
---
# <a name="filter-and-sort-data-in-a-windows-forms-application"></a>在 Windows 窗体应用程序中对数据进行筛选和排序

您可以通过将属性设置 <xref:System.Windows.Forms.BindingSource.Filter%2A> 为返回所需记录的字符串表达式来筛选数据。

您可以通过将属性设置 <xref:System.Windows.Forms.BindingSource.Sort%2A> 为要排序的列名称对数据进行排序; 追加 `DESC` 以降序排序，或按 `ASC` 升序排序。

> [!NOTE]
> 如果你的应用程序不使用 <xref:System.Windows.Forms.BindingSource> 组件，则可以使用对象对数据进行筛选和排序 <xref:System.Data.DataView> 。 有关详细信息，请参阅 [dataview](/dotnet/framework/data/adonet/dataset-datatable-dataview/dataviews)。

## <a name="to-filter-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件筛选数据

- 将 <xref:System.Windows.Forms.BindingSource.Filter%2A> 属性设置为要返回的表达式。 例如，以下代码将返回以 `CompanyName` "B" 开头的的客户：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet6":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet6":::

## <a name="to-sort-data-by-using-a-bindingsource-component"></a>使用 BindingSource 组件对数据进行排序

- 将 <xref:System.Windows.Forms.BindingSource.Sort%2A> 属性设置为要作为排序依据的列。 例如，下面的代码对列中的客户按 `CompanyName` 降序排序：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs" id="Snippet7":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb" id="Snippet7":::

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
