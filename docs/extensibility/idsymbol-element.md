---
title: IDSymbol 元素 |Microsoft Docs
description: IDSymbol 元素包含表示菜单、组或命令的 GUID： ID 对的 ID。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f59089ab981bc97100386b3e1907ef903ede3bd0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069837"
---
# <a name="idsymbol-element"></a>IDSymbol 元素
`IDSymbol`元素包含表示菜单、组或命令的 GUID： id 对的 id。 GUID 来自父 `GuidSymbol` 元素。 `IDSymbol`元素具有一个 `name` 属性，该属性提供 ID 的友好名称，该名称包含在属性中 `value` 。

## <a name="syntax"></a>语法

```xml
<IDSymbol name=ElementName value="0x0010" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|name|必需。 ID 符号的名称。|
|value|必需。 ID 符号的数字 ID 值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[GuidSymbol 元素](../extensibility/guidsymbol-element.md)|包含表示菜单、组或命令的 GUID： ID 对的 GUID。 对 `IDSymbol` 元素进行分组。|

## <a name="remarks"></a>备注
 `IDSymbol`给定元素中的每个元素 `GuidSymbol` 必须具有唯一的 `value` 。 但是， `IDSymbol` 具有相同值的元素可以存在于包中，只要它们具有不同的父元素。

## <a name="see-also"></a>另请参阅
- [Visual Studio 命令表 ( .vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
