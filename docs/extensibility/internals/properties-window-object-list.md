---
title: "\"属性\" 窗口对象列表 |Microsoft Docs"
description: 了解用于与 Visual Studio IDE 的属性窗口中的对象列表进行交互的接口。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Properties window, object list
ms.assetid: 6c159c9d-345d-4b23-8ddd-9839d338b62f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4ed4b3fc37d4110d6cd6dfd02c2dea503cbee194
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602567"
---
# <a name="properties-window-object-list"></a>属性窗口对象列表
" **属性** " 窗口中的对象列表是一个下拉列表，可用于将所选内容更改为在一个或多个选定窗口中可用的其他对象。 选择此列表中的不同对象将触发对的调用 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> ，以通知环境已选择了新的对象。 然后，将更改在 " **属性** " 窗口中显示的信息，以显示与新选择的对象相关联的属性。

## <a name="the-object-list"></a>对象列表
 对象列表包括两个字段：对象名称以粗体显示 () 和对象类型。

 以粗体显示的对象类型的对象名称是从对象本身使用接口提供的属性来检索的 `Name` <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>仅上的方法 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> 为该接口的 coclass 返回。 " **属性** " 窗口使用 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 来获取组件类的名称，该名称在下拉列表中显示为对象名称。

 如果该对象没有 `Name` 属性，则不会在对象列表的名称区域中显示名称。 如果希望在 "对象" 列表中显示名称，则可以将 "名称" 属性添加到对象。

 如果 COM 对象未实现 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> ，" **属性** " 窗口将显示接口名称，而不是列表左侧的对象名称。

## <a name="see-also"></a>另请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
