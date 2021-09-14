---
title: LocationField 元素（Visual Studio 项目模板）
titleSuffix: ''
description: 了解 LocationField 元素及其如何指定是启用、禁用还是隐藏项目模板的"Project"对话框"位置"文本框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationField
helpviewer_keywords:
- LocationField element [Visual Studio project templates]
ms.assetid: 6aaaa155-6ce0-4f7f-aa50-8d63d7a7c992
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f1ad5263f11cd7e940b641959de1dea393eb98ab
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664281"
---
# <a name="locationfield-element-visual-studio-project-templates"></a>LocationField (Visual Studio项目模板) 
指定"新建 **项目"对话框中** 的"位置Project是启用、禁用还是隐藏项目模板。

 \<VSTemplate> \<TemplateData>
 \<LocationField>

## <a name="syntax"></a>语法

```
<LocationField> Enabled/Disabled/Hidden </LocationField>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 对模板进行分类，并定义它在"新建"和"新建 **"Project。**|

## <a name="text-value"></a>文本值
 需要一个文本值。

 有效的文本值为：

- `Enabled`，指定 **启用"新建****Project"对话框** 的"位置"框。

- `Disabled`，指定 **已禁用"** 新建 **Project的"** 位置"框。

- `Hidden`，指定 **隐藏"新建****Project的"** 位置"框。

## <a name="remarks"></a>备注
 默认值为 `Enabled`。

 "**新建** 项目"对话框中的 **"Project"** 文本框允许用户更改保存新项目的默认目录。

 只有在基础项目系统支持该元素时，对话框 `Location` 才使用 元素中指定的值。

## <a name="example"></a>示例
 以下示例阐释 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 模板的元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <LocationField>Disabled</LocationField>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
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
