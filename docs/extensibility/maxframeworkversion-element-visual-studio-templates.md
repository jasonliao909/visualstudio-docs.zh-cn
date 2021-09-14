---
title: MaxFrameworkVersion 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 MaxFrameworkVersion 元素及其如何指定模板.NET Framework的最大版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <MaxFrameworkVersion> Element (Visual Studio Templates)
- MaxFrameworkVersion Element (Visual Studio Templates)
ms.assetid: f732a9d3-fc29-405b-9298-01ea83fc58b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 05d61e298c666d22df1af8d426cb0671feb8b9c5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664263"
---
# <a name="maxframeworkversion-element-visual-studio-templates"></a>MaxFrameworkVersion (Visual Studio模板) 

指定模板所需的.NET Framework的最大版本。 它确定"新建版本"对话框的"目标 **框架版本**"下拉列表中 **Project值。** 为了使用户能够选择框架版本，还必须指定[RequiredFrameworkVersion](../extensibility/requiredframeworkversion-element-visual-studio-templates.md) .NET Framework模板的最低版本。

> [!IMPORTANT]
> 从 Visual Studio 2017 版本 15.6 开始，"目标框架版本"下拉列表不再是"新建"对话框的"模板"部分中显示的模板 **Project** 筛选器。 相反 **，"目标框架版本** "下拉列表用作所选模板的框架选取器。

 \<VSTemplate> \<TemplateData>
 \<MaxFrameworkVersion>

## <a name="syntax"></a>语法

```xml
<MaxFrameworkVersion> ... </MaxFrameworkVersion>
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

 文本必须是模板允许的最大.NET Framework版本号。

## <a name="remarks"></a>备注

`MaxFrameworkVersion` 是可选元素。 除非需要元素，否则应省略元素，以便不要无意中限制模板.NET Framework `MaxFrameworkVersion` 支持的范围。 如果.NET Framework模板，则还应省略它。

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

此示例中，模板.NET Framework的最大版本为 `MaxFrameworkVersion` 4.7.1。 使用此模板创建的项目可以面向.NET Framework 4.7.1 版本。

## <a name="see-also"></a>请参阅

- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
