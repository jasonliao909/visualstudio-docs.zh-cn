---
title: 组合元素|Microsoft Docs
description: Combo 元素定义组合框中显示的命令。 有四种：DropDownCombo、DynamicCombo、IndexCombo 和 MRUCombo。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 431d68b6e545506f5fc90cc5a98a52dd4f1c33ad
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904949"
---
# <a name="combo-element"></a>组合元素
定义组合框中显示的命令。 有四种类型的组合框，如下所示：DropDownCombo、DynamicCombo、IndexCombo 和 MRUCombo。

## <a name="syntax"></a>语法

```xml
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">
  <Parent>... </Parent
  <CommandFlag>... </CommandFlag>
  <Strings>... </Strings>
</combo>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|GUID|必需。 GUID/ID 命令标识符的 GUID。|
|id|必需。 GUID/ID 命令标识符的 ID。|
|defaultWidth|必需。 一个整数，指定组合框的像素宽度。|
|idCommandList|必需。 发送到活动命令目标的 ID，用于检索要显示在组合框中的项的列表。 该 ID 与 控件在同一 GUID 范围内。|
|priority|可选。 一个指定优先级的数值。|
|type|可选。 一个枚举值，该值指定按钮的类型。<br /><br /> 如果未提供，则使用 Button。<br /><br /> DropDownCombo<br /> VSPackage 负责填写此组合框的内容。 用户无法在此下拉列表的文本框中键入任何内容。<br /><br /> DynamicCombo<br /> VSPackage 负责填写此组合框的内容。 用户可以编辑此组合，还可以选择该组合中的项。<br /><br /> IndexCombo<br /> 与 DynamicCombo 相同，只不过它引发项的索引而不是其文本。<br /><br /> MRUCombo<br /> 由集成开发环境 (IDE) VSPackage 填充。  用户可以在此组合框中进行编辑。 每个组合框的 IDE 最多记住最后 16 个条目。<br /><br /> 当用户在组合框中选择某些内容或输入新内容时，IDE 会通知相应的 VSPackage。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent|可选。 按钮的父元素。|
|CommandFlag|必需。 请参阅 [命令标志元素](../extensibility/command-flag-element.md)。 按钮的有效 CommandFlag 值如下所示。<br /><br /> - 区分大小写<br /><br /> - CommandWellOnly<br /><br /> - DefaultDisabled<br /><br /> - DefaultInvisible<br /><br /> - DynamicVisibility<br /><br /> - FilterKeys<br /><br /> - IconAndText<br /><br /> - NoAutoComplete<br /><br /> - NoButtonCustomize<br /><br /> - NoCustomize<br /><br /> - NoKeyCustomize<br /><br /> - StretchHorizontally|
|字符串|必需。 请参阅 [字符串元素](../extensibility/strings-element.md)。 必须定义子 ButtonText 元素。|
|Annotation|可选注释。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Commands 元素](../extensibility/commands-element.md)|表示 VSPackage 工具栏上的命令集合。|

## <a name="example"></a>示例

```xml
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>

<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"
  priority="0x0500" type="DropDownCombo" defaultWidth="100"
  idCommandList="cmdidGetInsertOptionsList">
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <ButtonText>Select Insert Options</ButtonText>
  </Strings>
</Combo>
```

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
