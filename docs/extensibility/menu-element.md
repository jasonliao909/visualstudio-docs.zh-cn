---
title: Menu 元素|Microsoft Docs
description: Menu 元素定义一个菜单项。 菜单类型为 Context、Menu、MenuController、MenuControllerLatched、Toolbar 和 ToolWindowToolbar。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Menus
- Menus element (VSCT XML schema)
ms.assetid: ce0560f3-b4c9-4ab2-a99c-d4e10f37b9e0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: edcfbaf05cc9590f020eb72d7bd0f7b5002d194b3f56ab7cab0127c3a5df1c0f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388544"
---
# <a name="menu-element"></a>Menu 元素
定义一个菜单项。 这六种类型的菜单：Context、Menu、MenuController、MenuControllerLatched、Toolbar 和 ToolWindowToolbar。

## <a name="syntax"></a>语法

```xml
<Menu guid="guidMyCommandSet" id="MyCommand" priority="0x100" type="button">
  <Parent>... </Parent>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Menu>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 一个数值，指定菜单在一组菜单中的相对位置。|
|ToolbarPriorityInBand|可选。 一个数值，指定停靠窗口时工具栏在带区中的相对位置。|
|类型|可选。 一个枚举值，该值指定元素类型。<br /><br /> 如果不存在，则默认类型为 Menu。<br /><br /> 上下文<br /> 用户右键单击窗口时显示的快捷菜单。 快捷菜单具有以下特征：<br /><br /> - 当菜单显示为 **快捷** 菜单 **时** ，不使用"父"和"优先级"字段。<br />- 可以用作子菜单，也可以用作快捷菜单。 在这种情况下，将同时 **使用"组 ID"** 和 **"优先级"** 字段。<br />- 并非始终可用。<br /><br /> 只有在满足以下条件时，才显示快捷菜单：<br /><br /> - 显示承载该窗口的窗口。<br />- VSPackage 中的鼠标处理程序检测到右键单击窗口，然后调用处理命令的方法。<br />- 通过调用 方法显示快捷菜单 (或 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager.ShowContextMenu%2A>) 方法 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A> 。<br /><br /> 菜单<br /> 提供下拉菜单。 下拉菜单具有以下特征：<br /><br /> - 在其定义中遵守父级。<br />- 组必须具有父组或 CommandPlacement。<br />- 可以是任何其他菜单中的子菜单。<br />- 每当显示其父菜单时，都会自动显示。<br />- 不需要实现任何 VSPackage 代码来显示它。<br /><br /> MenuController<br /> 提供通常在工具栏中使用的拆分按钮下拉菜单。 MenuController 菜单具有以下特征：<br /><br /> - 必须通过 Parent 或 CommandPlacement 包含在另一个菜单中。<br />- 在其定义中遵守父级。<br />- 可以将任何类型的菜单作为父级。<br />- 每当显示其父菜单时，都会自动提供。<br />- 无需编程支持即可显示菜单。<br /><br /> 拆分按钮菜单中的命令将显示在菜单按钮上。 显示的命令具有以下特征之一：<br /><br /> - 如果命令仍显示并启用，则它是最后使用的命令。<br />- 这是第一个显示的命令。<br /><br /> MenuControllerLatched<br /> 提供一个拆分按钮下拉菜单，可通过将命令标记为闩锁，将命令指定为默认选择。<br /><br /> 闩锁命令是在菜单中标记为选中的命令，通常通过显示一个选中标记。 如果命令在 接口的 方法的实现中设置了 OLECMDF_LATCHED 标志，则该命令 `QueryStatus` 可以标记为闩 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 锁。 MenuControllerLatched 菜单具有以下特征：<br /><br /> - 必须通过父组或 CommandPlacement 包含在另一个菜单中。<br />- 在其定义中遵守父级。<br />- 可以将任何类型的菜单作为父级。<br />- 每当显示父菜单时，都可用。<br />- 无需编程支持即可显示菜单。<br /><br /> 拆分按钮菜单中的命令将显示在菜单按钮上。 显示的命令具有以下特征之一：<br /><br /> - 这是已闩锁的第一个显示的命令。<br />- 这是第一个显示的命令。<br /><br /> 工具栏<br /> 提供工具栏。 工具栏具有以下特征：<br /><br /> - 忽略其定义中的 Parent。<br />- 不能成为任何组的子项，甚至不能使用 CommandPlacement。<br />- 始终可以通过单击"视图"菜单 **上的** "工具栏 **"来显示** 。<br />- 可以使用 [VisibilityItem 显示](../extensibility/visibilityitem-element.md)。<br />- 不需要任何代码来创建它。 有关如何创建工具栏的示例，请参阅 [添加工具栏](../extensibility/adding-a-toolbar.md)。<br /><br /> ToolWindowToolbar<br /> 提供附加到特定工具窗口的工具栏，就像工具栏附加到开发环境一样。<br /><br /> - 忽略其定义中的 Parent。<br />- 不能成为任何组的子项，甚至不能使用 CommandPlacement。<br />- 仅在显示承载工具栏的工具窗口并且 VSPackage 将工具栏显式添加到工具窗口时显示。 这通常在创建工具窗口时完成，方法是从工具窗口 (获取由接口) 表示的工具栏主机属性，然后 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost> 调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolWindowToolbarHost.AddToolbar%2A> 方法。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|Parent|可选。 菜单项的父元素。|
|CommandFlag|必需。 请参阅 [命令标志元素](../extensibility/command-flag-element.md)。 菜单的有效 CommandFlag 值如下所示：<br /><br /> -   **AlwaysCreate**<br />-   **DefaultDocked**<br />-   **DefaultInvisible** -此标志不会影响工具栏的显示。<br />-   **DontCache**<br />-   **DynamicVisibility** -此标志不会影响工具栏的显示。<br />-   **IconAndText**<br />-   **NoCustomize**<br />-   **NotInTBList**<br />-   **NoToolbarClose**<br />-   **TextChanges**<br />-   **TextIsAnchorCommand**|
|字符串|必需。 请参阅 [字符串元素](../extensibility/strings-element.md)。 `ButtonText`必须定义子元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|

## <a name="example"></a>示例

```
<Menu guid="cmdGuidWidgetCommands" id="menuIDEditWidget"
  priority="0x0002" type="Menu">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit"/>
  <CommandFlag>AlwaysCreate</CommandFlag>
  <Strings>
    <ButtonText>Edit Widget</ButtonText>
  </Strings>
</Menu>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
