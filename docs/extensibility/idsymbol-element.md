---
title: IDSymbol 元素|Microsoft Docs
description: IDSymbol 元素包含表示菜单、组或命令的 GUID：ID 对的 ID。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDSymbol element (VSCT XML schema)
- VSCT XML schema elements, IDSymbol
ms.assetid: 760cfd20-3c06-422c-9103-98bfa1f387f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 513033b2db2cbf222c7835679ad36e00b91887b6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122086893"
---
# <a name="idsymbol-element"></a>IDSymbol 元素
`IDSymbol`元素包含表示菜单、组或命令的 GUID：ID 对的 ID。 GUID 来自父 `GuidSymbol` 元素。 `IDSymbol`元素具有 `name` 一个 属性，该属性提供 ID 的友好名称，该名称包含在 `value` 属性中。

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
|value|必需。 ID 符号的数值 ID 值。|

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[GuidSymbol 元素](../extensibility/guidsymbol-element.md)|包含表示菜单、组或命令的 GUID：ID 对的 GUID。 对 `IDSymbol` 元素进行分组。|

## <a name="remarks"></a>备注
 给定 `IDSymbol` 元素中的 `GuidSymbol` 每个元素都必须具有唯一的 `value` 。 但是，只要元素具有不同的父元素，具有相同值的元素就可以 `IDSymbol` 存在于包中。

## <a name="see-also"></a>请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
