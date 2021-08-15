---
title: BuildProjectOnload 元素 (Visual Studio模板) |Microsoft Docs
description: 了解 BuildProjectOnload 元素，以及如何在创建新项目并将其添加到解决方案时仅生成新项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: b07d3074-0fc9-45e1-baf5-da6bd4f3f1c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9ca65dee11938f4152a30dedd25a3b4f3e566dd3b88e9e54da46579e30fa3243
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308358"
---
# <a name="buildprojectonload-element-visual-studio-templates"></a>BuildProjectOnload (Visual Studio模板) 
创建时仅生成新项目，并将其添加到解决方案中。 未生成整个解决方案。

元素层次结构：

```xml
<VSTemplate>
  <TemplateData>
    <BuildProjectOnLoad>
```

## <a name="syntax"></a>语法

```vb
<BuildProjectOnLoad> true/false </BuildProjectOnLoad>
```

## <a name="attributes-and-elements"></a>特性和元素
 下列各节描述了特性、子元素和父元素。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|`TemplateData`|对模板进行分类，并定义它在"新建项目"Project"**添加新** 项 **"对话框中的** 显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为 或 `true` `false` ，以指示是否在从模板创建新项目时仅生成新项目。

## <a name="remarks"></a>备注
 `BuildProjectOnLoad` 是可选元素。 默认值为 `false`。

## <a name="example"></a>示例
 以下示例演示了 Visual C# 模板的元数据。

```xml
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <BuildProjectOnload>true</BuildProjectOnLoad>
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

## <a name="see-also"></a>另请参阅

- [BuildOnLoad 属性和元素](buildonload-visual-studio-templates.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
