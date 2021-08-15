---
title: SupportsMasterPage 元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 SupportsMasterPage 元素及其如何指定是否在 "添加新项" 对话框中启用了 "选择母版页" 复选框。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#SupportsMasterPage
helpviewer_keywords:
- <SupportsMasterPage> element [Visual Studio Templates]
- SupportsMasterPage element [Visual Studio Templates]
ms.assetid: ce877a6a-9bba-4fd9-92fb-0a8dfec9e75b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4138f7ffdb227c0a7bacd09fb514d2d22c63d5962ab3c9787b616dedde3d8d38
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121320968"
---
# <a name="supportsmasterpage-element-visual-studio-templates"></a>SupportsMasterPage 元素（Visual Studio 模板）
指定是否在 "**添加新项**" 对话框中启用 "**选择母版页**" 复选框。

 \<VSTemplate> \<TemplateData>
 \<SupportsMasterPage>

## <a name="syntax"></a>语法

```
<SupportsMasterPage> true/false </SupportsMasterPage>
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
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|指定对模板进行分类的数据，并定义它在 "**新建 Project** " 或 "**新建项**" 对话框中的显示方式。|

## <a name="text-value"></a>文本值
 需要一个文本值。

 文本必须是 `true` 或 `false` ，指示是否在 "**添加新项**" 对话框中启用了 "**选择母版页**" 复选框。

## <a name="remarks"></a>备注
 `SupportsMasterPage` 是可选元素。 默认值是 `false`。

 `SupportsMasterPage`元素仅适用于 Web 项模板。

## <a name="example"></a>示例
 下面的示例演示了包含母版页支持的 Web 项目的元数据。

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
        <SupportsMasterPage>true</SupportsMasterPage>
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
- [创建 Project 和项模板](../ide/creating-project-and-item-templates.md)
