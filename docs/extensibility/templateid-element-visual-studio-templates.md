---
title: " (Visual Studio 模板) 的 TemplateID 元素 |Microsoft Docs"
description: 了解 TemplateID 元素以及它如何为通过 TemplateGroupID 元素分类到一组项模板的项模板指定标识符。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#TemplateID
helpviewer_keywords:
- <TemplateID> element [Visual Studio Templates]
- TemplateID element [Visual Studio Templates]
ms.assetid: 6ca24b4e-0325-4a9e-855e-0cbbe7361d8f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e33f2d5c424e5d48cff212dc736bbc13e58801d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056007"
---
# <a name="templateid-element-visual-studio-templates"></a>TemplateID 元素（Visual Studio 模板）
指定由 [TemplateGroupID](../extensibility/templategroupid-element-visual-studio-templates.md) 元素分类到一组项模板的项模板的标识符。

 \<VSTemplate> \<TemplateData>
 \<TemplateID>

## <a name="syntax"></a>语法

```
<TemplateID> ... </TemplateID>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 一个 `string` ，它表示由元素分类到一组项模板中的项模板的标识符 `TemplateGroupID` 。

## <a name="remarks"></a>备注
 `TemplateID` 是可选元素。

 如果 .vstemplate 文件省略了 `TemplateID` 元素，则 [Name](../extensibility/name-element-visual-studio-templates.md) 元素将用作模板的标识符。

 元素的值 `TemplateID` 与项目系统注册 (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\11.0\Projects一起使用 \\) 来筛选在 " **添加新项** " 对话框中显示的模板。

## <a name="see-also"></a>另请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
