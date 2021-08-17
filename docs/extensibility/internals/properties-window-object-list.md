---
title: 属性窗口对象列表|Microsoft Docs
description: 了解在 IDE 中用于与 属性窗口 对象Visual Studio的接口。
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
ms.openlocfilehash: 7ce39d335d48335408eea192c23bd5a091900a48055dcad0d65671b158b7b6e5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121275393"
---
# <a name="properties-window-object-list"></a>属性窗口对象列表
"属性"窗口中 **的对象** 列表是一个下拉列表，可用于将所选内容更改为一个或多个选定窗口中可用的其他对象。 从此列表中选择其他对象会触发对 的调用，以通知环境已 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 选择新对象。 然后，"属性 **"** 窗口中显示的信息将更改为显示与新选择的对象关联的属性。

## <a name="the-object-list"></a>对象列表
 对象列表由两个字段组成：以粗体 (显示的对象) 对象类型。

 使用 接口提供的 属性从对象本身检索以粗体显示的对象类型 `Name` 左侧显示 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 的对象名称。 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo.GetClassInfo%2A>（上的唯一方法 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> ） <xref:Microsoft.VisualStudio.OLE.Interop.ITypeInfo> 返回该接口的组件类。 " **属性** "窗口使用 获取 coclass 的名称，该名称在下拉列表中显示为 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 对象名称。

 如果对象没有 属性， `Name` 则名称不会显示在对象列表的"名称"区域中。 如果希望在对象列表中显示名称，可以将 Name 属性添加到 对象。

 如果 COM 对象未实现 ，"属性"窗口将显示接口名称，而不是列表左侧的对象 <xref:Microsoft.VisualStudio.OLE.Interop.IProvideClassInfo> 名称。 

## <a name="see-also"></a>请参阅
- [扩展属性](../../extensibility/internals/extending-properties.md)
