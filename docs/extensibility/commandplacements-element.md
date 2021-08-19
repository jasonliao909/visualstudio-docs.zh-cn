---
title: CommandPlacements 元素 |Microsoft Docs
description: CommandPlacements 元素将 CommandPlacement 元素和其他 CommandPlacements 组分组。 CommandPlacements 元素是可选的。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CommandPlacements
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 78a5724a-3b9f-4c78-9c0d-8faa3924f81c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 3ee3d626536ef16bc378be647b8418bb732ad8d6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122051282"
---
# <a name="commandplacements-element"></a>CommandPlacements 元素
CommandPlacements 元素将 CommandPlacement 元素和其他 CommandPlacements 组分组。

 CommandPlacements 元素是可选的。 如果辅助位置中必须不包含任何命令、组或菜单，则不需要在 *.vsct* 文件中包含此部分。

## <a name="syntax"></a>语法

```xml
<CommandPlacements>
  <CommandPlacement>... </CommandPlacement>
  <CommandPlacement>... </CommandPlacement>
</CommandPlacements>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|条件|可选。 请参阅 [条件特性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|CommandPlacements|将 CommandPlacement 元素和其他 CommandPlacements 分组分组。|
|[CommandPlacement 元素](../extensibility/commandplacement-element.md)|启用要包含在多个组或菜单中的按钮、组和菜单。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的所有元素。|

## <a name="example"></a>示例

```xml
<CommandPlacements>
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"
    priority="0x0300">
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>
  </CommandPlacement>
</CommandPlacements>
```

## <a name="see-also"></a>请参阅
- [CommandPlacement 元素](../extensibility/commandplacement-element.md)
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
