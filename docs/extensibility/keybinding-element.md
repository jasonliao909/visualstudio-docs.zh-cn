---
title: KeyBinding 元素|Microsoft Docs
description: KeyBinding 元素指定命令的键盘快捷方式。 命令可以同时具有与之关联的单键绑定和双键绑定。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6afd0a9658f088b66f2c18c632ffcd7b9a09f555
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898856"
---
# <a name="keybinding-element"></a>KeyBinding 元素
KeyBinding 元素指定命令的键盘快捷方式。

 命令可以同时具有与之关联的单键绑定和双键绑定。 单个键绑定的一个示例是 **"保存** + **"命令** 的Ctrl S。 双键绑定需要两个连续的键组合来触发命令。 双键绑定的一个示例是 <strong>Ctrl *+</strong> K <strong>，Ctrl</strong> <strong>+</strong> K** 用于设置书签。

## <a name="syntax"></a>语法

```
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|GUID|必需。|
|id|必需。|
|编辑器|必需。 编辑器 GUID 指示此键盘快捷方式将处于活动状态的编辑上下文。 全局绑定范围值为"guidVSStd97"。|
|key1|必需。 有效值包括所有可键入的字母数字，以及前面带有 0x 和 VK_constants 的两位数[十六进制VK_constants。](/windows/desktop/inputdev/virtual-key-codes)|
|mod1|可选。 **Ctrl、Alt** 和Shift 的任意组合 **，用** 空格分隔。|
|key2|可选。 有效值包括所有可键入的字母数字，以及前面带有 0x 和 VK_constants 的两位数[十六进制VK_constants。](/windows/desktop/inputdev/virtual-key-codes)|
|mod2|可选。 **Ctrl、Alt** 和Shift 的任意组合 **，用** 空格分隔。|
|模拟器|可选。|
|条件|可选。 请参阅 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)。|

### <a name="child-elements"></a>子元素

|元素|描述|
|-------------|-----------------|
|Parent||
|Annotation||

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[KeyBindings 元素](../extensibility/keybindings-element.md)|对 KeyBinding 元素和其他 KeyBindings 分组进行分组。|

## <a name="example"></a>示例

```
<KeyBindings>
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"
    editor="guidWidgetEditor" key1="VK_F5"/>
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>
</KeyBindings>
```

## <a name="see-also"></a>另请参阅
- [KeyBindings 元素](../extensibility/keybindings-element.md)
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
