---
title: SDKReference 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 SDKReference 元素及其如何指定项模板使用 SDK 引用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 72c8b352-0b7a-42b3-ba5d-2a2d1e90c34b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5ea070cf466782a1da09e1ba48d08a6965fd041a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602324"
---
# <a name="sdkreference-element-visual-studio-templates"></a>SDKReference 元素（Visual Studio 模板）
指定项模板使用 SDK 引用。

## <a name="syntax"></a>语法

```xml
<VSTemplate>
    <TemplateContent>
        <References>
            <Reference>
                <SDKReference>SDKname</SDKReference>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[引用](../extensibility/reference-element-visual-studio-templates.md)|指定向项目添加项时要添加的程序集引用。|

## <a name="text-value"></a>文本值
 需要一个文本值。

## <a name="remarks"></a>备注
 本文本指定实例化项模板时要向项目添加的 SDK 引用。

```xml
<VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
    <TemplateData> . . . </TemplateData>
    <TemplateContent>
        <References>
            <Reference>
                <SDKReference>Microsoft Visual C++ Runtime Package, Version=11.0.0.0</SDKReference>
...
```

## <a name="see-also"></a>另请参阅
- [References 元素（Visual Studio 模板）](../extensibility/references-element-visual-studio-templates.md)
- [Reference 元素（Visual Studio 模板）](../extensibility/reference-element-visual-studio-templates.md)
- [创建Project项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
