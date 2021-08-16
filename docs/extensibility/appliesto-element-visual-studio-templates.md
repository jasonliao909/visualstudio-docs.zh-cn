---
title: AppliesTo 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 AppliesTo 元素及其如何指定用于匹配一个或多个功能的可选表达式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 8fb1334b-d78c-405f-98b4-786e9f6b58d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 575a1a428c4d3e2816fcb275f6b1609ebf97bab7d4c56e51be3ad24e7f44d27a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434927"
---
# <a name="appliesto-element-visual-studio-templates"></a>AppliesTo (Visual Studio模板) 

指定一个可选表达式来匹配一个或多个功能 (请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.VsProjectCapabilityExpressionMatcher>) 。 功能由项目类型通过层次结构公开为属性 [__VSHPROPID5。VSHPROPID_ProjectCapabilities](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID5.VSHPROPID_ProjectCapabilities>)。 这使得具有公共适用功能的多个项目类型可以共享此模板。

此元素为可选元素。 一个模板文件中最多只能包含一个实例。 根据当前选择的活动项目的功能，此元素仅启用一个项模板以在适用时选择使用。 此元素无法用于设置不适用的项模板。 如果缺少 `AppliesTo` 或表达式未成功选择使用，则 `TemplateID` 或 `TemplateGroupID` 将用于使模板可用，如使用产品的早期版本一样。

在 Visual Studio 2013 Update 2 中引入。 若要引用正确的版本，请参阅引用在[Visual Studio 2013 SDK Update 2 中提供的程序集](/previous-versions/dn632168(v=vs.120))。

```xml
<VSTemplate>
   <TemplateData>
      <AppliesTo>
```

## <a name="syntax"></a>语法

```xml
<AppliesTo>Capability1</AppliesTo>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|对模板进行分类。|

## <a name="text-value"></a>文本值

需要一个文本值。 此文本指定项目的功能。

有效表达式语法按以下方式定义：

- 功能表达式，例如" (VisualC &#124; CSharp) + (MSTest &#124; NUnit) "。

- "&#124;"是 OR 运算符。

- "&"和"+"字符都是 AND 运算符。

- “!”字符是 NOT 运算符。

- 括号强制使用计算优先顺序。

- null 或空表达式作为匹配计算。

- Project可能是除以下保留字符之外的任何字符："''：;，+-*/ \\ ！~&#124;&%$@^ () = {} []<>？ \t\b\n\r

## <a name="example"></a>示例

下面的示例演示三个不同模板。 `Template1` 适用于所有 C# 项目类型或支持该功能的其他任何项目 `WindowsAppContainer` 类型。 `Template2` 适用于任何类型的所有 C# 项目。 `Template3` 适用于 `WindowsAppContainer` 项目以外的 C# 项目。

```xml
<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp | WindowsAppContainer</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 2 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp</AppliesTo>
    </TemplateData>
</VSTemplate>

<!--  Template 1 -->
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <AppliesTo>CSharp_Class + (!WindowsAppContainer)</AppliesTo>
    </TemplateData>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
