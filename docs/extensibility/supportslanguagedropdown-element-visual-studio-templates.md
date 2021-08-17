---
title: SupportsLanguageDropDown 元素（Visual Studio 模板）
titleSuffix: ''
description: 了解 SupportsLanguageDropDown 元素及其如何指定 Web 项模板对于多语言是否相同，以及是否启用了 Language 选项。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsLanguageDropDown
helpviewer_keywords:
- SupportsLanguageDropDown element [Visual Studio Templates]
- <SupportsLanguageDropDown> element [Visual Studio Templates]
ms.assetid: 641197d5-f724-4c06-bc47-2e22dad3fbfb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f02b7b70e3caedca11a41fd399ec80e84c4c8a39ccfc8eb98db795a4d49fa58b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413812"
---
# <a name="supportslanguagedropdown-element-visual-studio-templates"></a>SupportsLanguageDropDown 元素（Visual Studio 模板）

指定对于多种语言，Web 项模板是否相同，以及是否在 "**添加新项**" 对话框中启用了 **Language** 选项。

 \<VSTemplate> \<TemplateData>
 \<SupportsLanguageDropDown>

## <a name="syntax"></a>语法

```xml
<SupportsLanguageDropDown> true/false </SupportsLanguageDropDown>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 将此模板分类并定义此模板在 **“新建项目”** 或 **“添加新项”** 对话框中的显示方式。|

## <a name="text-value"></a>文本值

 需要一个文本值。

 文本必须是 `true` 或 `false` ，指示是否可从 "**添加新项**" 对话框中使用 "**语言**" 选项。

## <a name="remarks"></a>备注

 `SupportsLanguageDropDown` 是可选元素。 默认值是 `false`。

 `SupportsLanguageDropDown`元素仅适用于 Web 项模板。

 如果此元素的值设置为 `true` ，则该项模板对于所有编程语言均相同，并且在 "**添加新项**" 对话框中启用了 "**语言**" 选项。 利用此选项，您可以选择要从模板创建的新项的编程语言。

## <a name="example"></a>示例

 下面的示例指定显示 " **语言** " 下拉选项。

```xml
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsLanguageDropDown>true</SupportsLanguageDropDown>
    </TemplateData>
    <TemplateContent>
        <Project File="WebApplication.webproj">
            <ProjectItem>icon.ico</ProjectItem>
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>
            <ProjectItem>Default.aspx.cs</ProjectItem>
        </Project>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅

- [Visual Studio模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建 Project 和项模板](../ide/creating-project-and-item-templates.md)
