---
title: 隐藏元素 (Visual Studio模板) |Microsoft Docs
description: 了解 Hidden 元素及其如何指定模板是出现在新项目还是"添加新项"对话框中。
ms.custom: SEO-VS-2020
ms.date: 04/17/2019
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Hidden
helpviewer_keywords:
- Hidden element [Visual Studio project template]
ms.assetid: f37406b0-52e7-4f2c-aacf-bc8d7a4117b3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 99923825e2faaba211921eefc45096e65c5ee1908f5a5c07032c1522d683906e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448307"
---
# <a name="hidden-element-visual-studio-templates"></a>隐藏元素 (Visual Studio模板) 

指定模板是出现在新项目还是"添加新 **项"** 对话框中。

```xml
<VSTemplate>
    <TemplateData>
        <Hidden>
```

## <a name="syntax"></a>语法

```xml
<Hidden>true</Hidden>
<Hidden>false</Hidden>
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

需要一个文本值。

文本必须为 或 ，指示模板是否将显示在"新建项Project或"添加新项" `true` `false` 对话框中。  

## <a name="remarks"></a>备注

`Hidden` 是可选元素。

如果指定，则不需要元素的其他 `TemplateData` 子元素。

## <a name="example"></a>示例

下面的示例演示了 C# 模板的元数据。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <Hidden>true</Hidden>
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

- [模板架构引用](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
