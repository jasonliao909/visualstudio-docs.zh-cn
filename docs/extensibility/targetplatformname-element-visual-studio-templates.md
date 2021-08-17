---
title: TargetPlatformName 元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 TargetPlatformName 元素及其如何指定项目模板面向的平台。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 3a6b1f45-b5d6-418e-add1-87ee8f15033d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0d888b393f669305b03379e0d138ecfa5e75305981a0bec03f53424b95ad6ec0
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121358880"
---
# <a name="targetplatformname-element-visual-studio-templates"></a>TargetPlatformName 元素（Visual Studio 模板）
指定项目模板面向的平台。 此元素用于指定项目模板用于创建 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 应用。

## <a name="syntax"></a>语法

```xml
<VSTemplate>
    <TemplateData>
        <TargetPlatformName> OperatingSystem</TargetPlatformName>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[RequiredPlatformVersion](../extensibility/requiredplatformversion-element-visual-studio-templates.md)|指定项目模板面向的操作系统版本。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

## <a name="remarks"></a>备注
 文本必须为 **Windows**。

## <a name="example"></a>示例
 此示例指定项目模板面向 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本。

```xml
<VSTemplate Type="Project" Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
        <RequiredPlatformVersion>8</RequiredPlatformVersion>
    </TemplateData>
    <TemplateContent> </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [创建 Project 和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
