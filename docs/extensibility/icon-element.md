---
title: Icon 元素|Microsoft Docs
description: 了解 Icon 元素，该元素表示 Visual Studio IDE 扩展中使用的图标，其中包括所使用的位图和位图条中的槽的属性。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Icon
- Icon element (VSCT XML schema)
ms.assetid: 73c58fe3-d53c-4f4e-b025-29567c6cbb7c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 861bca1bc4a0f43f8e5165ae4fdf172fc858dfaf575683a921f52f3428e9c0d0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414670"
---
# <a name="icon-element"></a>Icon 元素
Icon 标记的 guid 属性是定义的位图的 guid。 `id`属性选择位图条中的槽。 此元素为可选元素。 如果未包含此元素，则 **隐含 guidOfficeIcon：msotcidNoIcon** 的值。

## <a name="syntax"></a>语法

```xml
<Icon guid="guidImages" id="bmpPic1" />
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|说明|
|---------------|-----------------|
|GUID|必需。 定义的位图的 guid。|
|id|必需。 选择位图条中的槽。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|无。|无。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[Buttons 元素](../extensibility/buttons-element.md)||

## <a name="see-also"></a>另请参阅
- [Visual Studio命令表 (.vsct) 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
