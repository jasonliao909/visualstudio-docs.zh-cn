---
title: References 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 References 元素及其如何对模板添加到项目的程序集引用进行分组。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#References
helpviewer_keywords:
- <References> element [Visual Studio Templates]
- References element [Visual Studio Templates]
ms.assetid: 1969146d-46bf-422d-8d46-0e9493925003
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9cf14c207d7ffb560612d963571fc11cca6d55e68ac4418afa8ec71bb69c0920
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359008"
---
# <a name="references-element-visual-studio-templates"></a>引用元素 (Visual Studio模板) 
对模板添加到项目的程序集引用进行分组。

 \<VSTemplate> \<TemplateContent>
 \<References>

## <a name="syntax"></a>语法

```xml
<References>
    <Reference>... </Reference>
    <Reference>... </Reference>
    ...
</References>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[引用](../extensibility/reference-element-visual-studio-templates.md)|必需的元素。<br /><br /> 指定向项目添加项时要添加的程序集引用。 元素中必须有一 `Reference` 个或多个 `References` 元素。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|指定模板的内容。|

## <a name="remarks"></a>备注
 `References` 是 `TemplateContent` 的可选子元素。

 和 `Reference` `References` 元素只能在特性值为 *的 .vstemplate* `Type` 文件中使用 `Item` 。

## <a name="example"></a>示例
 下面的示例演示项 `TemplateContent` 模板的 元素。 此 XML 添加对 *程序集System.dllSystem.Data.dll**的引用。*

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
