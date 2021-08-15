---
title: VisibilityItem 元素 |Microsoft Docs
description: VisibilityItem 元素确定命令和工具栏的静态可见性。 条目用于标识命令或菜单，以及关联的命令 UI 上下文。
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
`VisibilityItem`元素确定命令和工具栏的静态可见性。 每个条目标识一个命令或菜单，以及一个关联的命令 UI 上下文。 Visual Studio 检测命令、菜单和工具栏及其可见性，而不加载定义它们的 vspackage。 IDE 使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> 方法来确定命令用户界面上下文是否处于活动状态。

 加载 VSPackage 后，Visual Studio 应由 VSPackage （而不是）确定命令可见性 `VisibilityItem` 。 若要确定你的命令的可见性，可以实现 <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus> 事件处理程序或 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> 方法，具体取决于你实现命令的方式。

 `VisibilityItem`只有当关联的上下文处于活动状态时，才会显示具有元素的命令或菜单。 通过为每个命令上下文组合包含一项，可以将单个命令、菜单或工具栏与一个或多个命令 UI 上下文相关联。 如果命令或菜单与多个命令 UI 上下文相关联，则在任何一个关联的命令 UI 上下文处于活动状态时，命令或菜单都可见。

 `VisibilityItem`元素仅适用于命令、菜单和工具栏，不适用于组。 如果元素的父菜单处于活动状态，则该元素不具有相关的 `VisibilityItem` 元素。

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

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|上下文|必需。 命令在其中可见的 UI 上下文。|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素
 无

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)|`VisibilityConstraints`元素确定命令组和工具栏的静态可见性。|

## <a name="remarks"></a>备注
 标准 Visual Studio UI 上下文在 *Visual Studio SDK 安装路径*\VisualStudioIntegration\Common\Inc\vsshlids.h 文件以及 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids> 和类中定义 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> 。 在类中定义了一组更完整的 UI 上下文 <xref:Microsoft.VisualStudio.VSConstants> 。

## <a name="example"></a>示例

```xml
<VisibilityConstraints>
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"
    context="guidNotViewSourceMode"/>
</VisibilityConstraints>
```

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>
- <xref:Microsoft.VisualStudio.Shell.OleMenuCommand.BeforeQueryStatus>
- <xref:Microsoft.VisualStudio.VSConstants>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids>
- <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80>
- [VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)
- [Visual Studio 命令表 (。.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
