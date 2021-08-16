---
title: 父元素|Microsoft Docs
description: Parent 元素指定元素是按钮、组合框、菜单或组的父级。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 52f3f1986a6cba794d0a46f04668c1f40e787e11dc14da37d89e1a99c752bd0f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414111"
---
# <a name="parent-element"></a>父元素
按钮或组合框的父级只能是一个组。 菜单或组的父级可能是任何其他菜单或组。 在 [CommandPlacement 元素中](../extensibility/commandplacement-element.md)，此元素是必需的;在所有其他实例中，它是可选的。 如果省略此元素，则隐含 `Group_Undefined:0` 的父级。

## <a name="syntax"></a>语法

```xml
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|

### <a name="child-elements"></a>子元素
 无

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向集成开发环境提供的命令的所有元素 (IDE) 。 例如，菜单项、菜单、工具栏和组合框。|
|[Buttons 元素](../extensibility/buttons-element.md)|对 [Button 元素元素进行](../extensibility/button-element.md) 分组。|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|
|[Groups 元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
