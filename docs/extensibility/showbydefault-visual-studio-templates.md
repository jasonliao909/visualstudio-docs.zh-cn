---
title: 'ShowByDefault 元素 (Visual Studio模板) '
description: 了解 ShowByDefault 元素，以及设置为 false 时如何指定模板将仅在指定的 TemplateGroupID 下显示。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ShowByDefault
helpviewer_keywords:
- <ShowByDefault> element [Visual Studio Templates]
- ShowByDefault element [Visual Studio Templates]
ms.assetid: 7be783f6-0ef6-42bc-924a-df9a2eba7781
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ceef636c722d950a96e522286714a50ddfd7e7422335c8934affd928357c234a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400564"
---
# <a name="showbydefault-element-visual-studio-templates"></a>ShowByDefault 元素 (Visual Studio模板) 
如果 `false` 为 ，则指定模板将仅在指定的 [TemplateGroupID 下显示](../extensibility/templategroupid-element-visual-studio-templates.md)。

 \<VSTemplate> \<TemplateData>
 \<ShowByDefault>

## <a name="syntax"></a>语法

```
<ShowByDefault> true/false </ShowByDefault>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为 `true` 或 `false`。 如果为 true，则指定将对所有项目类型显示该模板。 如果为 false，则该将仅在指定的 `TemplateGroupID` 下显示该模板。

## <a name="remarks"></a>备注
 `ShowByDefault` 是可选元素。 默认值为 `true`。

## <a name="example"></a>示例
 以下示例阐释 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 模板的元数据。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <ShowByDefault>false</ShowByDefault>
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
- [创建Project项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [TemplateGroupID 元素（Visual Studio 模板）](../extensibility/templategroupid-element-visual-studio-templates.md)
