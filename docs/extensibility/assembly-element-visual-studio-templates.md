---
title: 程序集元素 (Visual Studio模板) |Microsoft Docs
titleSuffix: ''
description: 了解 Assembly 元素及其如何指定有关程序集的信息，模板使用该程序集向项目添加该程序集的引用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Assembly
helpviewer_keywords:
- Assembly element [Visual Studio templates]
- <Assembly> element [Visual Studio templates]
ms.assetid: 9242f76a-1273-4b8a-8f26-6606f91829ef
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 54fc5cfccde99776136f0cb904d02bf6a4971045
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664631"
---
# <a name="assembly-element-visual-studio-templates"></a>程序集元素 (Visual Studio模板) 
指定有关程序集的信息，模板使用该程序集向项目添加该程序集的引用。

 \<VSTemplate> \<TemplateContent>
 \<References>
 \<Reference>
 \<Assembly>

## <a name="syntax"></a>语法

```
<Assembly> AssemblyName </Assembly>
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

 此文本指定在实例化项模板时要添加到项目的程序集。 必须以下列方式之一指定此程序集名称：

- 作为完整的程序集名称。 例如：

    ```
    <Assembly>
        MyAssembly, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom = null.
    </Assembly>
    ```

- 作为简单文本引用。 例如：

    ```
    <Assembly> System </Assembly>
    ```

## <a name="remarks"></a>备注
 `Assembly` 是 `Reference` 的必需子元素。

 和 `Reference` `References,` `Assembly` 元素只能在特性值为 的 *.vstemplate* `Type` 文件中使用 `Item` 。

## <a name="example"></a>示例
 下面的示例演示项 `TemplateContent` 模板的 元素。 此 XML 添加对程序集 *System.dllSystem.Data.dll的引用*。 

```
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
