---
title: 引用元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 Reference 元素以及它如何指定在将项添加到项目时要添加的程序集引用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Reference
helpviewer_keywords:
- Reference element [Visual Studio templates]
- <Reference> element [Visual Studio templates]
ms.assetid: 852772ea-c324-42e9-8c8a-6d565414a109
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 84aed9d443e38e6d61069f919de115394d5f8450d56b0da930d95c1a915c08e1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121336678"
---
# <a name="reference-element-visual-studio-templates"></a>Visual Studio 模板 (引用元素) 
指定向项目添加项时要添加的程序集引用。

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>

## <a name="syntax"></a>语法

```xml
<Reference>
    <Assembly> ... </Assembly>
</Reference>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[程序集](../extensibility/assembly-element-visual-studio-templates.md)|必需的元素。<br /><br /> 指定有关程序集的信息，模板使用该程序集将该程序集的引用添加到项目。 `Assembly`每个元素中必须有一个元素 `Reference` 。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[参考](../extensibility/references-element-visual-studio-templates.md)|将模板添加到项目的程序集引用分组。|

## <a name="remarks"></a>备注
 `Reference` 是 `References` 的必需子元素。

 `Reference`和 `References` 元素只能在属性值为的 *.vstemplate* 文件中使用 `Type` `Item` 。

## <a name="example"></a>示例
 下面的示例演示 `TemplateContent` 项模板的元素。 此 XML 添加对 *System.dll* 和 *System.Data.dll* 程序集的引用。

```xml
<TemplateContent>
    <References>
        <Reference>
            <Assembly>
                System, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
        <Reference>
            <Assembly>
                System.Data, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089
            </Assembly>
        </Reference>
    </References>
    ...
</TemplateContent>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
