---
title: KeyBindings 元素|Microsoft Docs
description: KeyBindings 元素对 KeyBinding 元素和其他 KeyBindings 分组进行分组。 本文包含一个示例。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- KeyBindings
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBindings element (VSCT XML schema)
ms.assetid: 26a15d5c-ddea-4977-af7f-d795ff09c7ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 2ba02fee1d647dfd1813fdc0cf33588c553b5bce
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110288"
---
# <a name="keybindings-element"></a>KeyBindings 元素
KeyBindings 元素对 KeyBinding 元素和其他 KeyBindings 分组进行分组。

## <a name="syntax"></a>语法

```xml
<KeyBindings>
  <KeyBinding>... </KeyBinding>
  <KeyBinding>... </KeyBinding>
</KeyBindings>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[KeyBinding 元素](../extensibility/keybinding-element.md)|指定命令的键盘快捷方式。|
|[KeyBindings](../extensibility/keybindings-element.md)|对 KeyBinding 元素和其他 KeyBindings 分组进行分组。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[CommandTable 元素](../extensibility/commandtable-element.md)|定义表示命令的所有元素。|

## <a name="example"></a>示例

```xml
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>请参阅
- [KeyBinding 元素](../extensibility/keybinding-element.md)
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
