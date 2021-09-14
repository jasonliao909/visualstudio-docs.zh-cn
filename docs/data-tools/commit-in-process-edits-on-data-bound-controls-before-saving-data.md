---
title: 未提交的编辑
description: 在保存数据之前，在 Windows窗体控件上提交进程内编辑。 为窗体上的所有 BindingSource 组件调用 EndEdit。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- committing edited records
- data-bound controls, in-process edits
- DataBinding class, committing edited records
- hierarchical update, committing edited records
- BindingSource class, committing edited records
- EndEdit method
ms.assetid: 61af4798-eef7-468c-b229-5e1497febb2f
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 9e69734b43a0c959a724ee9116f919597c14002d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126601210"
---
# <a name="commit-in-process-edits-on-data-bound-controls-before-saving-data"></a>在保存数据前提交数据绑定控件中正在进行的编辑

在数据绑定控件中编辑值时，用户必须从当前记录中导航以将更新的值提交到控件绑定到的基础数据源。 将项从"数据源窗口 [](add-new-data-sources.md)"拖动到窗体上时，放置的第一项将生成代码到 的"**保存"按钮** 单击事件 <xref:System.Windows.Forms.BindingNavigator> 。 此代码调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 的 方法 <xref:System.Windows.Forms.BindingSource> 。 因此，只为添加到窗体的第一个 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> <xref:System.Windows.Forms.BindingSource> 生成对 方法的调用。

<xref:System.Windows.Forms.BindingSource.EndEdit%2A> 调用将提交当前正在编辑的任何数据绑定控件中的所有更改。 因此，如果数据绑定控件仍具有焦点，则单击“保存”按钮后，会先提交该控件中所有挂起的编辑，然后再执行真正的保存（`TableAdapterManager.UpdateAll` 方法）。

可以将应用程序配置为自动提交更改，即使用户在保存过程中尝试保存数据而不提交更改。

> [!NOTE]
> 设计器只 `BindingSource.EndEdit` 为放在窗体上的第一个项添加代码。 因此，必须添加一行代码，以调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 窗体上每个 的 <xref:System.Windows.Forms.BindingSource> 方法。 可以手动添加一行代码，以调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> 每个 的 方法 <xref:System.Windows.Forms.BindingSource> 。 或者，可以在执行保存之前将 方法添加到 `EndEditOnAllBindingSources` 窗体并调用它。

以下代码使用 [LINQ (语言 ](/dotnet/csharp/linq/) 集成查询) 查询来访问所有组件，并针对窗体上的每个组件 <xref:System.Windows.Forms.BindingSource> 调用 <xref:System.Windows.Forms.BindingSource.EndEdit%2A> <xref:System.Windows.Forms.BindingSource> 方法。

## <a name="to-call-endedit-for-all-bindingsource-components-on-a-form"></a>为窗体上的所有 BindingSource 组件调用 EndEdit

1. 将以下代码添加到包含组件的 <xref:System.Windows.Forms.BindingSource> 窗体。

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs" id="Snippet1":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb" id="Snippet1":::

2. 紧接在任何调用之前添加以下代码行，以将窗体 (`TableAdapterManager.UpdateAll()` 方法) ：

     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/CS/Form1.cs" id="Snippet2":::
     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/VSProDataOrcasEndEditOnAll/VB/Form1.vb" id="Snippet2":::

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [分层更新](../data-tools/hierarchical-update.md)
