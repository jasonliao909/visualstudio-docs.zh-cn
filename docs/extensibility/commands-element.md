---
title: Commands 元素|Microsoft Docs
description: Commands 元素表示 VSPackage 工具栏上的命令集合，可以包含以下部分：菜单、组、按钮、组合和位图。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Commands
helpviewer_keywords:
- Commands element (VSCT XML schema)
- VSCT XML schema elements, Commands
ms.assetid: 47cf16a5-d78b-452e-86f6-b5893856dddf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 35cea63308ffaef653904f4c959164bd09b73df0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146090"
---
# <a name="commands-element"></a>Commands 元素
表示 VSPackage 工具栏上的命令集合。 集合可以有最多五个子节，如下所示：菜单、组、按钮、组合和位图。

 每个子节子元素（例如 ）由唯一的命令 ID（GUID 和数字标识符对） \<Menu> 标识。 GUID 标识"命令集"，用于对逻辑相关的命令进行分组。 VSPackage 应定义自己的命令集，以避免与其他 VSPackage 定义的命令 ID 冲突。

## <a name="syntax"></a>语法

```xml
<Commands package="GuidMyPackage" >
  <Menus>... </Menus>
  <Groups>... </Groups>
  <Buttons>... </Buttons>
  <Combos>... </Combos>
  <Bitmaps>... </Bitmaps>
</Commands>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|包|一个 GUID，用于标识提供命令的 VSPackage。<br /><br /> 例如，package="guidVsPackage1Pkg"。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[菜单元素](../extensibility/menus-element.md)|定义 VSPackage 实现的所有菜单。|
|[Groups 元素](../extensibility/groups-element.md)|包含用于定义 VSPackage 中的命令组的条目。|
|[Buttons 元素](../extensibility/buttons-element.md)|对 Button 元素进行分组。|
|[Bitmaps 元素](../extensibility/bitmaps-element.md)|对位图元素进行分组。|
|[Combos 元素](../extensibility/combos-element.md)|对组合元素进行分组。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示 VSPackage 向 IDE 提供的命令的所有元素。 可能的元素包括菜单项、菜单、工具栏和组合框。|

## <a name="example"></a>示例
 下面的示例演示如何使用 [Commands 元素](../extensibility/commands-element.md)。

```
<Commands package="guidMyPackage">
    <Menus>
      <Menu Condition="'%(DEBUG)' != 'true'"
        guid="cmdSetGuidMyProductCommands" id="menuIDMainMenu"
        priority="0x0000" type="Menu">
        <Annotation>
          <Documentation>this is an annotation</Documentation>
          <AppInfo>
            <CustomData>
              <CustomSubElement>Some data</CustomSubElement>
            </CustomData>
          </AppInfo>
        </Annotation>
        <CommandFlag>AlwaysCreate</CommandFlag>
        <Strings>
          <ButtonText>MainMenu</ButtonText>
        </Strings>
      </Menu>
  </Menus>
<Commands>
```

## <a name="see-also"></a>请参阅
- [VSPackage 如何添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
