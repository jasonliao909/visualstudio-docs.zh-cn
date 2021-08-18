---
title: DefaultName 元素 (Visual Studio 模板) |Microsoft Docs
description: 了解 DefaultName 元素以及它如何指定 Visual Studio 项目系统在创建项目或项时将生成的名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#DefaultName
helpviewer_keywords:
- DefaultName element [Visual Studio project templates]
ms.assetid: 0ff056c8-b9d2-4747-9308-92adf1811491
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b26eced0849ebd4551c0f91f3ba2b7040022312c0e8007dc0a2cf54decc24788
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121377023"
---
# <a name="defaultname-element-visual-studio-templates"></a>DefaultName 元素 (Visual Studio 模板) 
指定 Visual Studio 项目系统在创建项目或项时为其生成的名称。

 \<VSTemplate> \<TemplateData>
 \<DefaultName>

## <a name="syntax"></a>语法

```
<DefaultName>
    Default Project Name
</DefaultName>
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

 此文本指定项目或项的默认名称。

## <a name="remarks"></a>备注
 `DefaultName` 是可选元素。

 对于项目，此元素指定在磁盘上存储项目的目录的名称。 对于项，它指定源文件的文件名。

 创建项目或项时，可以使用 "**名称**" 选项（可从 "**新建 Project** " 对话框或 "**添加新项**" 对话框获取）修改默认名称。

 如果你不希望项目系统生成项目或项的默认名称，请将 [ProvideDefaultName](../extensibility/providedefaultname-element-visual-studio-templates.md) 元素设置为 `False` 。

## <a name="example"></a>示例
 下面的示例演示了类的标准项模板的元数据 [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] 。

```
<VSTemplate Type="Item" Version="3.0.0"
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <Name>MyClass</Name>
        <Description>My custom C# class.</Description>
        <Icon>Icon.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <DefaultName>MyClass.cs</DefaultName>
    </TemplateData>
    <TemplateContent>
        <ProjectItem ReplaceParameters="true">MyClass.cs</ProjectItem>
    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>请参阅
- [Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)
- [创建项目和项模板](../ide/creating-project-and-item-templates.md)
