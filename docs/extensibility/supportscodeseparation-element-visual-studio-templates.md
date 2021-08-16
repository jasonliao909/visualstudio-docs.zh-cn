---
title: SupportsCodeSeparation 元素（Visual Studio 模板）
titleSuffix: ''
description: 了解 SupportsCodeSeparation 元素及其如何在"添加新项"对话框中指定是否启用"将代码放在单独的文件中"复选框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsCodeSeparation
helpviewer_keywords:
- SupportsCodeSeparation element [Visual Studio Templates]
- <SupportsCodeSeparation> element [Visual Studio Templates]
ms.assetid: 8112aac8-a269-40e5-b92b-9b9a6ff5a542
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1f33f86722621b6c069363f3136a62b497ed5d31a78c2744f5432bea1c44832
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121431443"
---
# <a name="supportscodeseparation-element-visual-studio-templates"></a>SupportsCodeSeparation 元素（Visual Studio 模板）
指定是否在"添加新项"对话框中启用"将代码放在单独的 **文件中"复选框**。

 \<VSTemplate> \<TemplateData>
 \<SupportsCodeSeparation>

## <a name="syntax"></a>语法

```
<SupportsCodeSeparation> true/false </SupportsCodeSeparation>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|必需的元素。<br /><br /> 对模板进行分类，并定义它在"新建项"Project或 **"** 新建项"**对话框中** 的显示。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须为 或 ，指示是否在"添加新项"对话框中启用"将代码放在 `true` `false` 单独的文件中"复选框。  

## <a name="remarks"></a>备注
 `SupportsCodeSeparation` 是可选元素。 默认值是 `false`。

 `SupportsCodeSeparation`元素仅适用于 Web 项模板。

 代码分离或代码隐藏页模型允许你将标记保留于一个文件中，将编程代码保留在另一个文件中。 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 和其他 .NET 语言使用此模型。

## <a name="example"></a>示例
 以下示例指定显示"将代码 **放在单独的文件中"** 选项。

```
<VSTemplate Version="3.0.0" Type="Project"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>
    <TemplateData>
        <Name>MyWebProjecStarterKit</Name>
        <Description>A simple Web template</Description>
        <Icon>icon.ico</Icon>
        <ProjectType>Web</ProjectType>
        <ProjectSubType>CSharp</ProjectSubType>
        <DefaultName>WebSite</DefaultName>
        <SupportsCodeSeparation>true</SupportsCodeSeparation>
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

## <a name="see-also"></a>另请参阅
- [Visual Studio模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建Project项模板](../ide/creating-project-and-item-templates.md)
