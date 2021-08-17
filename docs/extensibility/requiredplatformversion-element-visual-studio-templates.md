---
description: 指定项目模板正常运行所需的操作系统的最低版本。
title: RequiredPlatformVersion 元素（Visual Studio 模板）
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f5f72045fdfca073fbc740698c2eefe57a1a932f32751f9fe278e17c280fad9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388525"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>RequiredPlatformVersion 元素 (Visual Studio 模板) 

指定项目模板正常运行所需的操作系统的最低版本。 此元素用于创建应用程序的项目模板 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 。

 `RequiredPlatformVersion`该值与操作系统的版本直接进行比较。 如果 `RequiredPlatformVersion` 高于操作系统版本，则该模板不会显示在 "**新建 Project** " 对话框中。 若要为 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本指定模板，请将设置 `RequiredPlatformVersion` 为6.2.0。 若要为 [!INCLUDE[win81](../debugger/includes/win81_md.md)] 或更高版本指定模板，请将设置 `RequiredPlatformVersion` 为6.3.0。

 指定 `RequiredPlatformVersion` = 8 的模板与以前的客户 [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] 模板兼容。

 .Vstemplate TemplateData ...。TargetPlatformName RequiredPlatformVersion

## <a name="syntax"></a>语法

```xml
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>
```

## <a name="attributes-and-elements"></a>特性和元素

 无。

### <a name="attributes"></a>特性

 无。

### <a name="child-elements"></a>子元素

 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[TemplatePlatformName](../extensibility/templatedata-element-visual-studio-templates.md)|指定项目模板面向的平台。|

## <a name="text-value"></a>文本值

 需要一个文本值。

## <a name="remarks"></a>备注

 此文本指定模板所需的最低操作系统版本。

## <a name="example"></a>示例

 此示例指定项目模板面向 [!INCLUDE[win8](../debugger/includes/win8_md.md)] 或更高版本。

```xml
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>

    </TemplateData>
    <TemplateContent>

    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [TargetPlatformName 元素 (Visual Studio 模板) ](../extensibility/targetplatformname-element-visual-studio-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
