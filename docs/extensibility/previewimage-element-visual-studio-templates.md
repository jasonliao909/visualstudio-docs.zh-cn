---
title: " (Visual Studio 模板) 的 PreviewImage 元素 |Microsoft Docs"
description: 了解 PreviewImage 元素及其如何指定将在 "新建项目" 或 "添加新项" 对话框中显示的预览图像的文件名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e306f6453ca3abbc2ad881821254ca88a160d01b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99967275"
---
# <a name="previewimage-element-visual-studio-templates"></a> (Visual Studio 模板的 PreviewImage 元素) 
为将在 " **新建项目** " 或 " **添加新项** " 对话框中显示的预览图像指定预览图像作为文件名。

 \<VSTemplate> \<TemplateData>
 \<PreviewImage>

## <a name="syntax"></a>语法

```
<PreviewImage>"filename"</PreviewImage>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将模板分类并定义它在 " **新建项目** " 或 " **添加新项** " 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是表示文件名的字符串。

## <a name="remarks"></a>备注
 `PreviewImage` 是可选元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
