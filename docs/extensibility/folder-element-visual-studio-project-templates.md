---
title: 文件夹元素 (Visual Studio Project模板) |Microsoft Docs
description: 了解 Folder 元素及其如何指定将添加到项目的文件夹。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#Folder
helpviewer_keywords:
- Folder element [Visual Studio project templates]
ms.assetid: 558e3d41-0db5-4c44-82bb-6bb87892b093
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f06f0a5323073304bda5126351ad07373be66ae39a3947e5fb95c553f827b674
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432626"
---
# <a name="folder-element-visual-studio-project-templates"></a>文件夹元素 (Visual Studio项目模板) 
指定将添加到项目的文件夹。

 \<VSTemplate> \<TemplateContent>
 \<Project>
 \<Folder>

## <a name="syntax"></a>语法

```
<Folder Name="Project Folder">
    <Folder> ... </Folder>
    <ProjectItem> ... </ProjectItem>
</Folder>
```

## <a name="attributes-and-elements"></a>特性和元素
 以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

|属性|描述|
|---------------|-----------------|
|`Name`|必需的特性。<br /><br /> 项目文件夹的名称。|
|`TargetFolderName`|可选特性。<br /><br /> 指定从模板创建项目时要提供的文件夹的名称。 此属性可用于使用参数替换来创建文件夹名称，或者使用国际字符串命名文件夹，该字符串不能直接在 *.zip使用。*|

### <a name="child-elements"></a>子元素

|元素|说明|
|-------------|-----------------|
|`Folder`|指定要添加到项目的文件夹。 `Folder` 元素可以包含子 `Folder` 元素。|
|[ProjectItem](../extensibility/projectitem-element-visual-studio-item-templates.md)|指定要添加到项目的文件。|

### <a name="parent-elements"></a>父元素

|元素|描述|
|-------------|-----------------|
|[Project](../extensibility/project-element-visual-studio-templates.md)|[TemplateContent 的可选子元素](../extensibility/templatecontent-element-visual-studio-templates.md)。|

## <a name="remarks"></a>备注
 `Folder` 是 的可选子级 `Project` 。

 可以使用以下任一方法将项目项组织到模板中的文件夹中：

- 将文件夹包括在模板.zip文件，然后通过指定元素中的文件路径（不包含任何元素）将它们添加到 *.vstemplate* `ProjectItem` 文件中 `Folder` 的项目。 这是建议的方法。 例如：

     `...`

     `<ProjectItem>\Folder\item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 将文件夹包括在模板 *.zip文件，* 并将其添加到包含 元素的 *.vstemplate* 文件中 `Folder` 的项目。 例如：

     `...`

     `<Folder name="Folder">`

     `<ProjectItem>item.cs</ProjectItem>`

     `</Folder>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

- 不要将文件夹包括在模板 *.zip文件，* 而是使用 元素的 属性 `TargetFileName` 添加 `ProjectItem` 文件夹。 例如：

     `...`

     `<ProjectItem TargetFileName="\Folder\item.cs">item.cs</ProjectItem>`

     `<ProjectItem>Form1.cs</ProjectItem>`

     `...`

## <a name="example"></a>示例
 以下示例演示了应用程序项目模板的Windows [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 元数据。

```
<VSTemplate Type="Project" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>My template</Name>
        <Description>A basic template</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
    </TemplateData>
    <TemplateContent>
        <Project File="MyTemplate.csproj">
            <ProjectItem>Form1.cs<ProjectItem>
            <ProjectItem>Form1.Designer.cs</ProjectItem>
            <ProjectItem>Program.cs</ProjectItem>
            <Folder Name="Properties">
                <ProjectItem>AssemblyInfo.cs</ProjectItem>
                <ProjectItem>Resources.resx</ProjectItem>
                <ProjectItem>Resources.Designer.cs</ProjectItem>
                <ProjectItem>Settings.settings</ProjectItem>
                <ProjectItem>Settings.Designer.cs</ProjectItem>
            </Folder>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
- [ProjectItem 元素（Visual Studio 项模板）](../extensibility/projectitem-element-visual-studio-item-templates.md)
