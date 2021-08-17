---
title: 属性窗口按钮|Microsoft Docs
description: 了解默认显示在按钮工具栏上的按钮属性窗口按钮的实现。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, buttons
ms.assetid: bdd2e3a7-ae6e-4e88-be1a-e0e3b7ddbbcc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 25cea6a321fe7cf7365f179fd699553bd32b23e3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094576"
---
# <a name="properties-window-buttons"></a>属性窗口按钮
根据开发语言和产品类型，某些按钮默认显示在"属性"窗口的 **工具栏** 上。 所有情况下，都将显示 **"分类**"、 **按字母顺序** 排序 **的"** 属性"和" **属性页** "按钮。 在 Visual C# Visual Basic中，还会 **显示**"事件"按钮。 在某些Visual C++项目中，**将显示VC++消息**"和 **"VC** 替代"按钮。 可能会为其他项目类型显示其他按钮。 有关"属性"窗口中按钮 **的信息** ，请参阅 [属性窗口](../../ide/reference/properties-window.md)。

## <a name="implementation-of-properties-window-buttons"></a>属性窗口按钮的实现
 单击"分类 **"** 按钮时，Visual Studio对具有焦点的对象调用 接口，以便 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 按类别对属性进行排序。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties> 在呈现给 `IDispatch` "属性"窗口的 **对象上** 实现。

 有 11 个预定义的属性类别，它们具有负值。 可以定义自定义类别，但我们建议为其分配正值，以将它们与预定义类别区别。

 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.MapPropertyToCategory%2A>方法返回指定属性的适当属性类别值。 <xref:Microsoft.VisualStudio.Shell.Interop.ICategorizeProperties.GetCategoryName%2A>方法返回包含类别名称的字符串。 只需为自定义类别值提供支持，Visual Studio标准属性类别值。

 单击"按字母 **顺序"** 按钮时，属性按名称的字母顺序显示。 根据本地化排序 `IDispatch` 算法检索名称。

 当" **属性** "窗口打开时 **，"属性** "按钮将自动显示为选中状态。 在环境的其他部分，将显示相同的按钮，你可以单击它以显示"属性 **"** 窗口。

 如果未 **为** 所选对象实现 ， `ISpecifyPropertyPages` 则"属性页"按钮不可用。 属性页显示通常与解决方案和项目关联的与配置相关的属性，但它们也可以与项目项相关联 (例如，在 Visual C++) 。

> [!NOTE]
> 无法使用非托管代码将工具栏按钮添加到"属性"窗口。 若要添加工具栏按钮，必须创建派生自 的托管对象 <xref:System.Windows.Forms.Design.PropertyTab> 。

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
