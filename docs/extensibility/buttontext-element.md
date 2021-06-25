---
title: ButtonText 元素|Microsoft Docs
description: 使用 ButtonText 元素可以指定各种菜单中显示的文本。 即使指定了其他文本字段，ButtonText 元素也不能为空。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ButtonText element (VSCT XML schema)
- VSCT XML schema elements, ButtonText
ms.assetid: 56aba884-0356-4894-ae4e-32d3938f6865
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf20a6876dd7ba52413a11f30a3d0130b32e535d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900704"
---
# <a name="buttontext-element"></a>ButtonText 元素
使用此字段可以指定各种菜单中显示的文本。 默认情况下，该 `ButtonText` 元素显示在菜单控制器中。 如果 `ButtonText` 其他文本字段为空，则 元素也将成为默认值。 即使 `ButtonText` 指定了其他文本字段，元素也不能为空。

## <a name="syntax"></a>语法

```xml
<ButtonText>My Command</ButtonText>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Strings 元素](../extensibility/strings-element.md)|对文本元素（如 和 ） `ButtonText` 进行分组 `CommandName` 。|

## <a name="text-value"></a>文本值
 元素的文本值提供为菜单项、组合和其他用户界面显示的文本，这些用户界面 (UI) `ButtonText` 具有可见文本的元素。

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
