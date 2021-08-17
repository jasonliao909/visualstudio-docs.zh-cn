---
title: 属性显示网格|Microsoft Docs
description: 了解属性名称和属性值字段在网格中的位置属性窗口以及如何在扩展属性时使用网格。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- properties [Visual Studio SDK], grid
ms.assetid: 318e41b0-acf5-4842-b85e-421c9d5927c5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: d6ed5ce8863cef32c787d86a5d78c423d78fef4f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057195"
---
# <a name="properties-display-grid"></a>属性显示网格

" **属性** "窗口显示网格中的字段。 左侧列包含属性名称;右侧列包含属性值。

## <a name="work-with-the-grid"></a>使用网格

双列列表显示可在设计时更改的配置无关属性及其当前设置。 请注意，可能不会显示所有属性。 例如，可以通过实现 方法将属性设置为隐藏 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> 。 具体而言，若要隐藏具有子属性的属性，

1. 将 `pfDisplay` 中的 参数设置为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.DisplayChildProperties%2A> `FALSE` 。

2. 将 `pfHide` 中的 参数设置为 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HideProperty%2A> `TRUE` 。

若要将信息推送到 **"属性"** 窗口，IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 。 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>VSPackages 会针对每个窗口调用 ，该窗口包含可选择的对象以及"属性"窗口中要显示 **的相关属性。** **解决方案资源管理器** 调用的 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 实现 `GetProperty` [__VSHPROPID。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>) 层次结构中，以获取层次结构中的可浏览对象。

如果 VSPackage 不支持 [__VSHPROPID。VSHPROPID_BrowseObject](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject>)，IDE 尝试使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> [__VSHPROPID。VSHPROPID_SelContainer](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_SelContainer>) 层次结构项或项提供的信息。

项目 VSPackage 不需要创建，因为实现它的 IDE 提供的窗口包 (例如，解决方案资源管理器) <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer>  <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 构造。

<xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer> 由 IDE 调用的三种方法组成：

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.CountObjects%2A>包含要显示在"属性"窗口中 **的对象数。**

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 返回 `IDispatch` 要显示在"属性"窗口中 **的选定** 对象。

- <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.SelectObjects%2A> 使 用户可以选择由 返回 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 的任何对象。 这样，VSPackage 可以直观地更新在 UI 中向用户显示的选择。

" **属性** "窗口从 对象 `IDispatch` 中提取信息，以检索正在浏览的属性。 "属性"浏览器使用 通过查询 从 获取的 来询问对象它 `IDispatch` `ITypeInfo` 支持哪些属性 `IDispatch::GetTypeInfo` 。 然后，浏览器使用这些值填充" **属性"** 窗口，并更改网格中显示的各个属性的值。 属性信息在 对象本身中维护。

由于返回的对象支持 ，因此调用方可以通过调用 或 ，使用表示所需信息的 DISPID (调度标识符 `IDispatch` `IDispatch::Invoke` `ITypeInfo::Invoke`) 获取对象名称等信息。 声明的 DISPID 为负数，以确保它们不与用户定义的标识符冲突。

" **属性** "窗口显示不同类型的字段，具体取决于所选对象的特定属性的属性。 这些字段包括编辑框、下拉列表和指向自定义编辑器对话框的链接。

- 枚举列表中包含的值由对 的 <xref:Microsoft.VisualStudio.Shell.Interop.ISelectionContainer.GetObjects%2A> 查询检索 `IDispatch` 。 通过双击字段名称，或者单击值，然后从下拉列表中选择新值，可以在属性网格中更改从枚举列表获取的值。 对于具有枚举列表中的预定义设置的属性，双击"属性"列表中的属性名称会循环访问可用选项。 对于只有两个选项的预定义属性（例如 true/false），请双击属性名称以在选项之间切换。

- 如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.HasDefaultValue%2A> `false` 为 ，则指示值已更改，该值以粗体文本显示。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing.CanResetPropertyValue%2A> 用于确定值是否可重置为原始值。 如果是这样，可以通过右键单击值，然后从显示的菜单中选择"重置"， **更改** 回默认值。 否则，必须手动将值更改回默认值。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsPerPropertyBrowsing> 还允许本地化和隐藏在设计期间显示的属性的名称，但不会影响运行时显示的属性名称。

- 单击省略号 (...) 按钮将显示属性值列表，用户可以从中选择 (如颜色选取器或字体列表) 。 <xref:Microsoft.VisualStudio.Shell.Interop.IProvidePropertyBuilder> 提供这些值。

## <a name="see-also"></a>请参阅

- [扩展属性](../../extensibility/internals/extending-properties.md)
