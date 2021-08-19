---
title: CommandPlacement 元素|Microsoft Docs
description: CommandPlacement 元素允许按钮、组和菜单包含在多个组或菜单中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 95a690ce394e088e3e490aa7e279725ff69bbdd1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122058027"
---
# <a name="commandplacement-element"></a>CommandPlacement 元素
CommandPlacement 元素允许按钮、组和菜单包含在多个组或菜单中。 通过使用 CommandPlacement 元素，不需要完全重新定义这些项，以便修改用户界面的外观。

 有关详细信息，请参阅 [创建可重用的按钮组](../extensibility/creating-reusable-groups-of-buttons.md)。

## <a name="syntax"></a>语法

```
<CommandPlacement guid="guidMyCommandSet" id="MyCommand" priority="0x001" >
  <Parent>... </Parent>
</CommandPlacement>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 命令集的 guid，如 [Symbols 元素 中定义](../extensibility/symbols-element.md)。|
|id|必需。 要放置的菜单、组或命令的 ID，如 中定义 `Symbols Element` 。|
|priority|必需。 确定项在其父元素中的可视位置。|
|条件|可选。 请参阅 [条件 Aattributes](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|Parent|必需。 承载要放置的项的菜单或组。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandPlacements 元素](../extensibility/commandplacements-element.md)|指定 CommandPlacements 和 CommandPlacement 元素的组。|

## <a name="example"></a>示例

```
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>请参阅
- [CommandPlacements 元素](../extensibility/commandplacements-element.md)
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
