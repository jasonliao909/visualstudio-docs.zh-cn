---
title: Groups 元素|Microsoft Docs
description: Groups 元素包含用于定义 VSPackage 命令组的条目。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Groups
- Groups element (VSCT XML schema)
ms.assetid: 740ca4ec-79fa-4b98-8f9a-2a137f9f7f98
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f20e19e19539e71a4dbed74a0dd5bb9af62a15f
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902821"
---
# <a name="groups-element"></a>Groups 元素
包含定义 VSPackage 的命令组的条目。

## <a name="syntax"></a>语法

```xml
<Groups>
  <Group>... </Group>
  <Group>... </Group>
</Groups>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|[Group 元素](../extensibility/group-element.md)|表示单个命令组。|
|[Groups 元素](../extensibility/groups-element.md)|包含定义 VSPackage 的命令组的条目。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令集合。|

## <a name="example"></a>示例

```xml
<Groups>
  <Group guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
    <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_MAINMENU"/>
  </Group>
</Groups>
```

## <a name="see-also"></a>另请参阅
- [VSPackages 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
