---
title: “浏览并选择 .NET 类型”对话框
description: 了解如何使用“浏览并选择 .NET 类型”对话框从工作流设计器中的程序集和项目的树视图中选择类型。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- TypeBrowser.UI
- ActivityTypeResolver.UI
ms.assetid: 864b60b6-a070-4e5c-aa5b-a25341b57ea6
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-workflow-designer
ms.workload:
- dotnet
ms.openlocfilehash: b0258a69738f340ca8a2a58d1c3b900171625e5d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602208"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>“浏览并选择 .NET 类型”对话框

在“属性”窗口、对话框或设计器（如变量设计器）中，当从数据类型列表中选择“浏览类型”时，将显示“浏览并选择 .NET 类型”对话框（以缩写形式称为“类型浏览器”）。 在此对话框中，可以从程序集和项目的树视图中选择类型。

在很多用户方案中都使用此对话框，这些方案包括：

- 设置变量或参数的类型时。

- 为一般活动选择类型时。

- 在 <xref:System.Activities.Statements.TryCatch> 活动上添加一个 catch 时。

> [!NOTE]
> 类型浏览器可以显示 Visual Basic 交错数组类型，但不显示多维数组类型。 有关详细信息，请参阅[交错数组](/previous-versions/visualstudio/visual-studio-2008/hkhhsz9t(v=vs.90))和[多维数组](/previous-versions/visualstudio/visual-studio-2008/d2de1t93(v=vs.90))。

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

1. 在“类型名称”框中，输入要使用的类型的名称。

2. 执行下列操作之一：

    - 要使用的类型的名称出现在“类型名称”框的树中之后，双击该类型以将其选中。

    - 在“类型名称”框中键入可唯一标识要使用类型的足够字符，然后按 Enter 键以选择该类型

### <a name="to-select-a-generic-type-from-the-type-browser"></a>从类型浏览器中选择一个泛型类型

1. 在“类型名称”框中，键入要使用的类型的名称。

2. 要使用的类型的名称出现在“类型名称”框的树中之后，单击该类型以将其选中，以便出现下拉框。

     选择要使用的类型以关闭下拉框中的泛型类型，然后单击“确定”。

## <a name="types-displayed-in-the-type-browser"></a>类型浏览器中显示的类型

类型浏览器中显示的类型可能因启动类型浏览器的方式而有所不同。 如果从“vs2010”中的工作流项目启动类型浏览器，则默认情况下，显示引用程序集以及引用项目中的所有类型。 如果从“vs2010”项目系统外（如在重新承载的工作流应用程序或独立的工作流文件中）启动类型浏览器，则默认情况下，显示在 AppDomain 中加载的所有程序集中的类型。

可以按活动设计器开发人员筛选类型浏览器中的类型。 对于任何给定的活动，您可能只看到一个类型子集。 例如，在 <xref:System.Activities.Statements.TryCatch> 活动中，只有从 <xref:System.Exception> 派生的类型显示在类型浏览器中。

## <a name="filtering-search-results-in-the-type-browser"></a>在类型浏览器中筛选搜索结果

键入的用于查找匹配的字符越多，“类型名称”框中的类型列表就会越短。 只有其完全限定名以你键入的字符串开头的类型或者其简短名称以你键入的字符串开头的类型会显示在筛选出的列表中。

例如：

1. 键入 Operation 将匹配 <xref:System.OperationCanceledException>，而非 <xref:System.InvalidOperationException>。 若要匹配 <xref:System.InvalidOperationException>，请开始键入 System.I 或 Invalid。

2. 键入 Generic 将匹配 <xref:System.GenericUriParser>，而非 <xref:System.Collections.Generic> 命名空间中的类型。 若要在 <xref:System.Collections.Generic> 命名空间中搜索类型，请键入该命名空间的完全限定名称。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>使用类型浏览器对话框选择服务协定

选择服务协定类型时，类型浏览器只显示具有 <xref:System.ServiceModel.ServiceContractAttribute> 特性的类型。

## <a name="see-also"></a>另请参阅

- [使用活动设计器](control-flow-activity-designers.md)
