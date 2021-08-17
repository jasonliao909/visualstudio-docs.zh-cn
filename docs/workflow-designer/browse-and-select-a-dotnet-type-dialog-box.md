---
title: “浏览并选择 .NET 类型”对话框
description: 了解如何使用 "浏览并选择 .NET 类型" 对话框从工作流设计器中的程序集和项目的树视图中选择类型。
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
ms.openlocfilehash: f14fe6095011e77341803c0cdeda5bcd94f0eb8805644859b5c2d6d4e8709481
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121423756"
---
# <a name="browse-and-select-a-net-type-dialog-box"></a>“浏览并选择 .NET 类型”对话框

在 " **属性** " 窗口、对话框或设计器（如变量设计器）中，当你从数据类型列表中选择 " **浏览类型** " 时，将为 " **浏览并选择 .net 类型** " 对话框 (在缩写形式中称为 "类型浏览器" ) 。 在此对话框中，可以从程序集和项目的树视图中选择类型。

在很多用户方案中都使用此对话框，这些方案包括：

- 设置变量或参数的类型时。

- 为一般活动选择类型时。

- 在 <xref:System.Activities.Statements.TryCatch> 活动上添加一个 catch 时。

> [!NOTE]
> 类型浏览器可以显示 Visual Basic 交错数组类型，但不显示多维数组类型。 有关详细信息，请参阅 [交错数组](/previous-versions/visualstudio/visual-studio-2008/hkhhsz9t(v=vs.90)) 和 [多维数组](/previous-versions/visualstudio/visual-studio-2008/d2de1t93(v=vs.90)) 。

## <a name="selecting-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

### <a name="to-select-a-value-or-reference-type-from-the-type-browser"></a>从类型浏览器中选择值或引用类型

1. 在 " **类型名称** " 框中，输入要使用的类型的名称。

2. 执行下列操作之一：

    - 一旦要使用的类型的名称出现在树中的 " **类型名称** " 框中，请双击该类型以将其选中。

    - 在 " **类型名称** " 框中键入足够多的字符来唯一标识要使用的类型，然后按 enter 键以选择类型

### <a name="to-select-a-generic-type-from-the-type-browser"></a>从类型浏览器中选择一个泛型类型

1. 在 " **类型名称** " 框中，键入要使用的类型的名称。

2. 一旦要使用的类型的名称出现在树中的 " **类型名称** " 框中，请单击相应的类型将其选择为 "导致" 下拉框。

     从下拉框中选择要用于关闭 "常规" 的类型，然后单击 **"确定"**。

## <a name="types-displayed-in-the-type-browser"></a>类型浏览器中显示的类型

类型浏览器中显示的类型可能因启动类型浏览器的方式而有所不同。 如果类型浏览器是从 **vs2010** 内的工作流项目启动的，则默认情况下将显示引用的程序集中的所有类型和引用的项目。 如果类型浏览器是从 **vs2010** 项目系统的外部启动 (例如，在重新承载工作流应用程序中，或者在独立工作流文件) 中启动的，则会显示在 AppDomain 中加载的所有程序集中的类型。

可以按活动设计器开发人员筛选类型浏览器中的类型。 对于任何给定的活动，您可能只看到一个类型子集。 例如，在 <xref:System.Activities.Statements.TryCatch> 活动中，只有从 <xref:System.Exception> 派生的类型显示在类型浏览器中。

## <a name="filtering-search-results-in-the-type-browser"></a>在类型浏览器中筛选搜索结果

键入更多字符以查找匹配项时，" **类型名称** " 框中的类型列表将变短。 只有其 fullyqualified 名称以您键入的字符串开头的类型或其短名称以您键入的字符串开头的类型才会显示在筛选列表中。

例如：

1. 键入 **操作** 匹配 <xref:System.OperationCanceledException> ，但不匹配 <xref:System.InvalidOperationException> 。 若要匹配 <xref:System.InvalidOperationException>，请开始键入 System.I 或 Invalid。

2. 键入 <xref:System.GenericUriParser> 命名空间中的泛型匹配项，而不是类型 <xref:System.Collections.Generic> 。 若要在命名空间中搜索类型 <xref:System.Collections.Generic> ，请键入命名空间的完全限定名称。

## <a name="selecting-a-service-contract-using-the-type-browser-dialog"></a>使用类型浏览器对话框选择服务协定

选择服务协定类型时，类型浏览器只显示具有 <xref:System.ServiceModel.ServiceContractAttribute> 特性的类型。

## <a name="see-also"></a>请参阅

- [使用活动设计器](control-flow-activity-designers.md)
