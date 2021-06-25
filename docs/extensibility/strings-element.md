---
title: Strings 元素|Microsoft Docs
description: Strings 元素包含 ButtonText 子元素和其他可选子元素。 文本字符串中的一个和指定键盘快捷方式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Strings element (VSCT XML schema)
- VSCT XML schema elements, Strings
ms.assetid: 23a42074-a689-481d-824f-b43aa448f266
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 27a649c7d3a8bb808153c280921d2304de59c379
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899402"
---
# <a name="strings-element"></a>Strings 元素
Strings 元素必须至少包含 **ButtonText** 子元素。 所有其他子元素是可选的。 无效的 XML 字符（如"&"和"<"）必须编码为实体 ("和""等 &amp; &lt;) 。

 文本字符串中的一个和指定命令的键盘快捷方式。

## <a name="syntax"></a>语法

```
<Strings>
  <ButtonText>... </ButtonText>
  <CommandName>... </CommandName>
</Strings>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|语言|可选。 Language="."。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|ButtonText|使用此字段和命令定义中的以下五个文本字段，可以指定显示在各种菜单中的文本。 默认情况下，该字段 `ButtonText` 显示在菜单控制器中。 如果 `ButtonText` 其他文本字段为空，则字段也将成为默认值。 即使 `ButtonText` 指定了其他文本字段，字段也不能为空。|
|ToolTipText|`ToolTipText`字段指定菜单项的工具提示中显示的文本。<br /><br /> 如果 `ToolTipText` 字段为空， `ButtonText` 则使用 字段。|
|MenuText|字段指定命令在主菜单、工具栏、快捷菜单或子菜单中显示 `MenuText` 的文本。 如果 `MenuText` 字段为空，则 IDE (集成) 使用 `ButtonText` 字段。 `MenuText`字段还可用于本地化。<br /><br /> 对于快捷菜单，字段是"快捷菜单"工具栏中显示的名称，可在 `MenuText` IDE 中自定义快捷菜单。 因此，请具体指定快捷菜单的名称;例如，使用"小组件包快捷菜单"而不是"快捷方式"。<br /><br /> 如果 `MenuText` 未指定字段，则 `ButtonText` 使用 字段。|
|CommandName|字段指定在"自定义"对话框的"命令"选项卡的键盘类别中显示的文本 (单击"工具"菜单上的"自定义 `CommandName` ") 。    |
|CanonicalName|"英语"字段以英文文本指定命令的名称，可在"命令"窗口中输入该名称以 `CanonicalName` 执行菜单项。  IDE 会去除不是字母、数字、下划线或嵌入句点的任何字符。 然后，此文本将串联 `ButtonText` 到 字段以定义命令。 例如 **，"文件"菜单** 上的 **"** 新建项目"将成为命令 File.NewProject。<br /><br /> 如果未指定英语字段，IDE 将使用 字段，并去除除字母、数字、下划线和嵌入句 `CanonicalName` `ButtonText` 点之外的所有字符。 例如，按钮文本"&定义命令..."变为 DefineCommands，其中将删除与号、空格和省略号。<br /><br /> 如果指定了 标志并更改了命令的文本，则"命令"窗口识别的相应命令不会更改;它仍然是原始或英语字段 `TextChanges`  `ButtonText` 的规范 `CanonicalName` 形式。|
|LocCanonicalName|字段 `LocCanonicalName` 的行为与英语字段相同 `CanonicalName` ，但允许指定本地化的命令文本。 可同时指定这两个规范字段。 由于 IDE 只分析在"命令"窗口中输入的文本，并与之关联命令，因此英语和非英语文本都可以与同一命令相关联。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Button 元素](../extensibility/button-element.md)|定义用户可与之交互的元素。|
|[Menu 元素](../extensibility/menu-element.md)|定义单个菜单项。|
|[Combo 元素](../extensibility/combo-element.md)|定义组合框中显示的命令。|

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表格 (.Vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
