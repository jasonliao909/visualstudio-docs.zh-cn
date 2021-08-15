---
title: WizardData 元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 WizardData 元素及其如何指定自定义 XML。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#WizardData
helpviewer_keywords:
- WizardData element [Visual Studio Templates]
- <WizardData> element [Visual Studio Templates]
ms.assetid: d0403a16-5d07-4fe5-b474-19ae3d9fd3ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d51d9827c5edcbcf522eb206add4769a8583f34ac7aa72732b472523e197bb6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121400434"
---
# <a name="wizarddata-element-visual-studio-templates"></a>WizardData 元素（Visual Studio 模板）

指定自定义 XML

```xml
\<VSTemplate>
\<WizardData>
```

## <a name="syntax"></a>语法

```xml
<WizardData>
    <!-- XML to pass to the custom wizard extension -->
    ...
</WizardData>
```

## <a name="attributes-and-elements"></a>特性和元素

以下各部分描述了特性、子元素和父元素。

### <a name="attributes"></a>特性

无。

### <a name="child-elements"></a>子元素

无。

### <a name="parent-elements"></a>父元素

|元素|说明|
|-------------|-----------------|
|[VSTemplate](../extensibility/vstemplate-element-visual-studio-templates.md)|必需的元素。<br /><br /> 包含项目模板、项模板或初学者工具包的所有元数据。|

## <a name="text-value"></a>文本值

文本值是可选的。

此文本指定要传递给 [WizardExtension](../extensibility/wizardextension-element-visual-studio-templates.md) 元素中指定的自定义向导扩展的自定义 XML。

## <a name="remarks"></a>备注

可以在此元素中指定任何 XML。 XML 将作为参数传递到自定义向导扩展，允许扩展使用此元素的内容。 不对此数据执行任何验证。

在方法中参数的字符串字典中， **WizardData** 元素的内容以不更改的形式传递 `IWizard.RunStarted` 。 字典键的名称为 `$wizarddata$` 。

## <a name="example"></a>示例

下面的示例演示 c # Windows 应用程序的标准项目模板的元数据。

```xml
<VSTemplate Version="3.0.0" Type="Item"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyTemplate</Name>
        <Description>Template using IWizard extension</Description>
        <Icon>TemplateIcon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
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
    <WizardExtension>
        <Assembly>MyWizard, Version=1.0.3300.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, Custom=null</Assembly>
        <FullClassName>MyWizard.CustomWizard</FullClassName>
    </WizardExtension>
    <WizardData>
        <!-- XML to pass to the custom wizard extension -->
    </WizardData>
</VSTemplate>
```

## <a name="see-also"></a>另请参阅

- [Visual Studio模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建 Project 和项模板](../ide/creating-project-and-item-templates.md)
- [WizardExtension 元素（Visual Studio 模板）](../extensibility/wizardextension-element-visual-studio-templates.md)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
