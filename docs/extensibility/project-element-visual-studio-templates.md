---
title: Project元素 (Visual Studio模板) |Microsoft Docs
description: 了解 Project 元素及其如何指定要添加到项目中的文件或目录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Project
helpviewer_keywords:
- Project element [Visual Studio Templates]
- <Project> element [Visual Studio Templates]
ms.assetid: 1da15ea6-26e2-462b-a03e-584ef4996579
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 260b52b23be9857cc3850824b3eda8fe795abb701c21788df7b487ae6f5e111c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121388521"
---
# <a name="project-element-visual-studio-templates"></a>Project元素 (Visual Studio模板) 
指定要添加到项目的文件或目录。

 \<VSTemplate> \<TemplateContent>
 \<Project>

## <a name="syntax"></a>语法

```
<Project
    File="MyProject.proj"
    TargetFileName="MyTargetProject.proj"
    ReplaceParameters="true/false">
    IgnoreProjectParameter="$myCustomParameter$"
        ...
</Project>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|`File`|必需的特性。<br /><br /> 指定模板中项目文件的名称 *.zip文件。*|
|`ReplaceParameters`|可选特性。<br /><br /> 一个布尔值，指定项目文件是否具有从模板创建项目时必须替换的参数值。 默认值为 `false`。|
|`TargetFileName`|可选特性。<br /><br /> 指定从模板创建项目时项目文件的名称。|
|`IgnoreProjectParameter`|可选特性。<br /><br /> 指定项目是否应该添加到当前解决方案。 如果参数替换文件中存在自定义参数"$*myCustomParameter*$"的值，则项目将创建，但不作为当前打开解决方案的一部分添加。|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|[文件夹](../extensibility/folder-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件夹。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md)|可选元素。<br /><br /> 指定要添加到项目的文件。|

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[TemplateContent](../extensibility/templatecontent-element-visual-studio-templates.md)|必需的元素。|

## <a name="remarks"></a>备注
 `Project` 是 `TemplateContent` 的可选子元素。

 `Project`元素用于指定项目，因此，仅在项目模板中有效。

 `Project` 元素可以具有 [Folder](../extensibility/folder-element-visual-studio-project-templates.md) 子元素或 [ProjectItem](../extensibility/projectitem-element-visual-studio-project-templates.md) 子元素，但不能同时包含 和 `Folder` `ProjectItem` 子元素。

 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]根据用户在"新建文件"对话框中输入的名称自动重命名 **Project** 名称。 如果要为使用模板创建的项目文件提供备用文件名，请使用 `TargetFileName` 属性。

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
- [ProjectItem 元素 (Visual Studio项目模板) ](../extensibility/projectitem-element-visual-studio-project-templates.md)
- [文件夹元素 (Visual Studio项目模板) ](../extensibility/folder-element-visual-studio-project-templates.md)
