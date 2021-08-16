---
title: CreateNewFolder 元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 CreateNewFolder 元素及其如何确定是否检查要在其中创建项目的目标目录是否不存在。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#CreateNewFolder
helpviewer_keywords:
- CreateNewFolder element [Visual Studio project templates]
ms.assetid: acef2016-4140-45d6-ace8-b8160eabd676
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dd332fe32044cb66f24418be016cdf75c9683d0ace936417cfecd8cf246a7e8c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403510"
---
# <a name="createnewfolder-element-visual-studio-templates"></a>CreateNewFolder 元素 (Visual Studio 模板) 
确定是否检查要创建项目的目标目录不存在。 如果该目录存在，则为项目创建新目录。 该设置通常由所有通用项目类型用来确定是否在新目录中创建新项目的 `NewProjectRequiresNewFolder(VsTemplate)` 注册表标志 (`HKEY_LOCAL_MACHINE/SOFTWARE(/Wow6432Node)/Microsoft/VisualStudio/<version number>/Projects/<project GUID>`) 重写。

 \<VSTemplate> \<TemplateData>
 \<CreateNewFolder>

## <a name="syntax"></a>语法

```
<CreateNewFolder>
    true/false
</CreateNewFolder>
```

## <a name="type"></a>类型
 `Boolean`

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

 此文本必须是 `true` 或 `false`，以指示从此模板创建项目时是否应创建一个新的容器文件夹。

## <a name="remarks"></a>备注
 `CreateNewFolder` 是可选元素。 默认值是 `true`。

 `CreateNewFolder` 元素中指定的值仅由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 使用（如果基础项目系统支持它）。

## <a name="example"></a>示例
 下面的代码示例指定从此模板创建项目时不创建新的文件夹。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <CreateNewFolder>false</CreateNewFolder>
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
