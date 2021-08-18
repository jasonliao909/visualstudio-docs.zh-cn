---
title: GuidSymbol 元素|Microsoft Docs
description: GuidSymbol 元素包含表示菜单、组或命令的 GUID：ID 对的 GUID。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, GuidSymbol
- GuidSymbol element (VSCT XML schema)
ms.assetid: 11fb3545-8974-4776-9a54-6b6e7739ae31
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: b79b8d9399e4294a4e22cbc36f11bccbf703e215
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086971"
---
# <a name="guidsymbol-element"></a>GuidSymbol 元素
`GuidSymbol`元素包含表示菜单、组或命令的 GUID：ID 对的 GUID。 ID 来自 `IDSymbol` 元素中的 `GuidSymbol` 元素。 `GuidSymbol`元素具有 `name` 一个 属性，该属性提供 GUID 的友好名称，该名称包含在 `value` 属性中。

## <a name="syntax"></a>语法

```xml
<GuidSymbol name="guidMyCommandSet" value="{xxxxxxxxxxxxx-xxxx-xxxx-xxxxxxxxxxxx}">
  <IDSymbol>... </IDSymbol>
  <IDSymbol>... </IDSymbol>
</GuidSymbol>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|name|必需。 GUID 符号的名称。|
|value|必需。 GUID 符号的 GUID。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[IDSymbol 元素](../extensibility/idsymbol-element.md)|包含表示菜单、组或命令的 GUID：ID 对的 ID。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Symbols 元素](../extensibility/symbols-element.md)|对 `GuidSymbol` *.vsct 文件中的元素进行* 分组。|

## <a name="remarks"></a>备注
 通常 *，.vsct* 文件在其 节中包含三个元素，一个元素用于包本身，一个元素用于命令集 (包提供) 的菜单、组和命令集合，另一个元素用于为按钮和其他可视组件提供图标的位图。 `GuidSymbol` `Symbols` 给定 `IDSymbol` 元素中的 `GuidSymbol` 每个元素都必须具有唯一的 `value` 。但是，只要元素具有不同的父元素，具有相同值的元素就可以 `IDSymbol` 存在于包中。

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
