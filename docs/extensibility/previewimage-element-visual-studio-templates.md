---
title: PreviewImage 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 PreviewImage 元素及其如何指定将在"新建"或"添加新项"对话框中Project图像的文件名。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a0ddae8f246ccedb6ca004743e7e18c22b38a0ddb4dabb671d55f07140274074
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431586"
---
# <a name="previewimage-element-visual-studio-templates"></a>PreviewImage (Visual Studio模板) 
指定预览图像作为文件名，用于预览图像，该预览图像将显示在"新建 **Project或"** 添加新 **项"对话框中**。

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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 对模板进行分类，并定义它在"新建项"Project **或"** 添加新项"**对话框中的显示** 方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是表示文件名的字符串。

## <a name="remarks"></a>备注
 `PreviewImage` 是可选元素。

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
