---
title: Button 元素|Microsoft Docs
description: Button 元素定义用户可与之交互的元素。 按钮可以是不同类型的：Button、MenuButton 和 SplitDropDown。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Buttons element (VSCT XML schema)
- VSCT XML schema elements, Buttons
ms.assetid: 96dccf51-2b00-4700-9d28-924b34c21ecd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9ad9551e15d3d64b899e2c7e70bf80597193973f0cecc04f2145cf0ecdc4d1c6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452636"
---
# <a name="button-element"></a>Button 元素
定义用户可与之交互的元素。 按钮可以是不同类型的：Button、MenuButton 和 SplitDropDown。

## <a name="syntax"></a>语法

```
<Button guid="guidMyCommandSet" id="MyCommand" priority="0x102" type="button">
  <Parent>... </Parent>
  <Icon>... </Icon>
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</Button>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|priority|可选。 一个指定优先级的数值。|
|类型|可选。 一个枚举值，该值指定按钮类型。<br /><br /> 如果未提供，则使用 Button。<br /><br /> Button<br /> 工具栏上显示的标准命令通常 (菜单、菜单和上下文菜单) 按钮。<br /><br /> MenuButton<br /> 不执行命令但生成另一个菜单的菜单项。<br /><br /> SplitDropDown<br /> 控件，如标准工具栏上的"撤消"和"重做"Microsoft Word。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[父元素](../extensibility/parent-element.md)|可选。 按钮的父元素。|
|[Icon 元素](../extensibility/icon-element.md)|可选。 与按钮关联的图标。|
|[命令标志元素](../extensibility/command-flag-element.md)|必需。 按钮的有效 CommandFlag 值如下所示。<br /><br /> - AllowParams<br /><br /> - CommandWellOnly<br /><br /> - DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> - DontCache<br /><br /> - DynamicItemStart<br /><br /> - DynamicVisibility<br /><br /> - FixMenuController<br /><br /> - IconAndText<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - NoShowOnMenuController<br /><br /> - Pict<br /><br /> - PostExec<br /><br /> - ProfferedCmd<br /><br /> - RouteToDocs<br /><br /> - TextCascadeUseBtn<br /><br /> - TextMenuUseButton<br /><br /> - TextChanges<br /><br /> - TextChangesButton<br /><br /> - TextContextUseButton<br /><br /> - TextMenuCtrlUseMenu<br /><br /> - TextMenuUseButton<br /><br /> - TextOnly|
|[Strings 元素](../extensibility/strings-element.md)|必需。 必须定义 [子 ButtonText](../extensibility/buttontext-element.md) 元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Buttons 元素](../extensibility/buttons-element.md)|对 Button 元素进行分组。|

## <a name="example"></a>示例
 以下示例在 *.vsct 文件中定义一个* 按钮。

 ```xml
<Button guid="guidMenuTextCmdSet" id="cmdidMyCommand" priority="0x0100" type="Button">
    <Parent guid="guidMenuTextCmdSet" id="MyMenuGroup" />
    <Icon guid="guidImages" id="bmpPic1" />
    <CommandFlag>TextChanges</CommandFlag>
    <Strings>
          <CommandName>cmdidMyCommand</CommandName>
          <ButtonText>My Command name</ButtonText>
    </Strings>
</Button>
 ```

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
