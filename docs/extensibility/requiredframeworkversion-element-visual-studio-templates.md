---
description: 指定模板所需的.NET Framework版本。
title: RequiredFrameworkVersion 元素（Visual Studio 模板）
titleSuffix: ''
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <RequiredFrameworkVersion> (Visual Studio Templates)
- RequiredFrameworkVersion (Visual Studio Templates)
ms.assetid: 08a4f609-51a5-4723-b89f-99277fb18871
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5164202c10008112b6072b1a45aed7d52c3ddf0598c97f6b69b32ba1cb9aadf4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305186"
---
# <a name="requiredframeworkversion-element-visual-studio-templates"></a>RequiredFrameworkVersion (Visual Studio模板) 

指定模板所需的.NET Framework版本。 这会导致"**新建框架版本"** 对话框中显示"目标框架 **Project** 下拉列表。 `RequiredFrameworkVersion`元素还确定下拉列表中可用的最低值。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本 15.6开始，"目标框架版本"下拉列表不再是"新建"对话框的"模板"部分中显示的模板 **Project** 筛选器。 相反，下拉列表用作所选模板的框架选取器。

 \<VSTemplate> \<TemplateData>
 \<RequiredFrameworkVersion>

## <a name="syntax"></a>语法

```xml
<RequiredFrameworkVersion> .... </RequiredFrameworkVersion>
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

 文本必须是模板所需的.NET Framework版本号。

## <a name="remarks"></a>备注

`RequiredFrameworkVersion` 是可选元素。 只有当模板支持特定的最低版本或更高版本时 (此元素（如果) 版本.NET Framework。 如果指定 元素，并且模板不支持特定最低版本的 .NET Framework，则"目标框架版本"下拉列表将在不适用时 `RequiredFrameworkVersion` 显示。 

## <a name="example"></a>示例

下面的示例演示标准类模板的 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 元数据。

```xml
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class template.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>3.0</RequiredFrameworkVersion>
        <MaxFrameworkVersion>4.7.1</MaxFrameworkVersion>
        <DefaultName>MyClass</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem>MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

此示例中，模板所需的.NET Framework版本（由 表示） `RequiredFrameworkVersion` 为 3.0。 使用此模板创建的项目可以面向.NET Framework 3.0 开始的版本。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [框架定位概述](../ide/visual-studio-multi-targeting-overview.md)
