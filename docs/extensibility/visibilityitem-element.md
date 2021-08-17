---
title: VisibilityItem 元素|Microsoft Docs
description: VisibilityItem 元素确定命令和工具栏的静态可见性。 条目标识命令或菜单以及关联的命令 UI 上下文。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VisibilityItem element (VSCT XML schema)
- VSCT XML schema elements, VisibilityItem
ms.assetid: 0932f551-972d-4194-84bb-426e3e4375e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 973e9403895d69af4d6d2f5a0384fd9f153d64d4506cd3cb9ba64d9e6c350e37
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121335259"
---
# <a name="visibilityitem-element"></a>VisibilityItem 元素
`VisibilityItem`元素确定命令和工具栏的静态可见性。 每个条目都标识一个命令或菜单，以及一个关联的命令 UI 上下文。 Visual Studio检测命令、菜单和工具栏及其可见性，而无需加载定义它们的 VSPackage。 IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> 方法确定命令 UI 上下文是否处于活动状态。

 加载 VSPackage 后，Visual Studio命令可见性由 VSPackage 而不是 确定 `VisibilityItem` 。 若要确定命令的可见性，可以实施事件处理程序或 方法，具体取决于 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 实现命令的方式。

 只有关联的上下文处于活动状态时，才显示具有 元素 `VisibilityItem` 的命令或菜单。 可以通过包含每个命令上下文组合的条目，将单个命令、菜单或工具栏与一个或多个命令 UI 上下文关联。 如果命令或菜单与多个命令 UI 上下文相关联，则当任一关联的命令 UI 上下文处于活动状态时，该命令或菜单都可见。

 `VisibilityItem`元素仅适用于命令、菜单和工具栏，而应用于组。 一个没有相关元素的元素在其父菜单处于活动状态 `VisibilityItem` 时可见。

## <a name="syntax"></a>语法

```xml
<VisibilityItem
  guid="cmdGuidMyProductCommands"
  id="cmdidAddWidget"
  context="guidNotViewSourceMode"/>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|上下文|必需。 命令可见的 UI 上下文。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)|`VisibilityConstraints`元素确定命令和工具栏组的静态可见性。|

## <a name="remarks"></a>备注
 标准 Visual Studio UI 上下文在 *Visual Studio SDK* 安装路径 \VisualStudioIntegration\Common\Inc\vsshlids.h 文件中以及 和 类中 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> 定义。 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> 类中定义了一组更完整的 UI <xref:Microsoft.VisualStudio.VSConstants> 上下文。

## <a name="example"></a>示例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)
- [Visual Studio命令表 (。Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
