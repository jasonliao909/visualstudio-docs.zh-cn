---
title: ProjectType 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 ProjectType 元素及其如何对项目模板进行分类，以便它出现在"新建Project或"添加新项"对话框中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectType
helpviewer_keywords:
- ProjectType element [Visual Studio project templates]
ms.assetid: ccf9d83f-c7f3-49c7-a31f-e1f22bec004c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 92fa66c122d441ed50e4ab83a4e0bfcce5c2e411372e97b45f747663cfc457c9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400928"
---
# <a name="projecttype-element-visual-studio-templates"></a>ProjectType 元素 (Visual Studio模板) 
对项目模板进行分类，以便它显示在"新建项目"或 **"Project"****对话框中的** 指定组下。

> [!WARNING]
> Project 2012 开始，C++ 支持Visual Studio模板。 在 2010 和更早版本中，C++ Visual Studio支持它们。

 \<VSTemplate> \<TemplateData>
 \<ProjectType>

## <a name="syntax"></a>语法

```xml
<ProjectType> CSharp/VisualBasic/VC/Web </ProjectType>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 此值指定模板将创建的项目类型，并且必须包含以下值之一：

- `CSharp`：指定模板创建项目 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 或项。

- `VisualBasic`：指定模板创建项目 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 或项。

- `Web`：指定模板创建 Web 项目或项。 如果 `ProjectType` 元素包含此值，则项目或项的语言在[ProjectSubType 元素中定义 (Visual Studio模板) 。 ](../extensibility/projectsubtype-element-visual-studio-templates.md)

## <a name="remarks"></a>备注
 `ProjectType` 是 `TemplateData` 的必需子元素。

 元素的值指定模板在"新建项"或"Project `ProjectType` 项"对话框中的位置。  例如，值为 的模板显示在"新建"对话框 `ProjectType` `CSharp` 的 **"Visual C#"Project** 下。 

 可以使用 [ProjectSubType](../extensibility/projectsubtype-element-visual-studio-templates.md) 元素指定模板子类型。

## <a name="example"></a>示例
 以下示例显示了应用程序的项目模板的 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic starter kit</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyStarterKit.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <ProjectItem>Properties\AssemblyInfo.cs</ProjectItem>
            <ProjectItem>Properties\Resources.resx</ProjectItem>
            <ProjectItem>Properties\Resources.Designer.cs</ProjectItem>
            <ProjectItem>Properties\Settings.settings</ProjectItem>
            <ProjectItem>Properties\Settings.Designer.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [ProjectSubType 元素 (Visual Studio模板) ](../extensibility/projectsubtype-element-visual-studio-templates.md)
