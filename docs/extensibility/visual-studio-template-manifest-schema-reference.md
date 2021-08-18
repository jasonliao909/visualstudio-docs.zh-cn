---
title: Visual Studio模板清单架构参考|Microsoft Docs
description: 此架构参考描述为项目Visual Studio项模板生成的模板清单Visual Studio的格式。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: bc7d0a81-0df5-41a9-a912-1b30e5da1d13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4e0cb5372340bfd3ca624d3c9844bd34ef1e0914
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122109937"
---
# <a name="visual-studio-template-manifest-schema-reference"></a>Visual Studio模板清单架构参考
此架构描述为项目或Visual Studio模板 (*生成的 .vstman*) 模板清单Visual Studio的格式。 该架构还描述了模板的位置和其他相关信息。

 ：由于存在单独的项和项目模板目录，因此清单不应混合使用项模板和项目模板。

> [!IMPORTANT]
> 此清单从 2017 Visual Studio开始提供。

## <a name="vstemplatemanifest-element"></a>VSTemplateManifest 元素
 清单的根元素。

### <a name="attributes"></a>特性

- **版本**：表示模板清单版本的字符串。 必需。

- **区域设置**：表示模板清单区域设置或区域设置的字符串。 区域设置值适用于所有模板。 必须针对每个区域设置使用单独的清单。 可选。

### <a name="child-elements"></a>子元素

- **VSTemplateContainer** 选。

- **VSTemplateDir** 选。

### <a name="parent-element"></a>父元素
 无。

## <a name="vstemplatecontainer"></a>VSTemplateContainer
 模板清单元素的容器。 清单定义的每个模板都有一个模板容器。

### <a name="attributes"></a>特性
 **VSTemplateType：** 一个字符串值，指定模板类型 (、 或 `"Project"` `"Item"` `"ProjectGroup"`) 。 必需

### <a name="child-elements"></a>子元素

- **RelativePathOnDisk：** 磁盘上模板文件的相对路径。 此位置还定义模板在"新建项"或"新建项 **"Project** 中显示的 **模板树** 中的位置。 对于部署为目录和单个文件的模板，此路径引用包含模板文件的目录。 对于部署为.zip *文件的模板*，此路径应为该 *.zip的路径。*

- **VSTemplateHeader：描述标头的 [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md) 元素。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="vstemplatedir"></a>VSTemplateDir
 描述模板所在的目录。 清单可以包含多个 **VSTemplateDir** 条目，为目录提供本地化的名称和排序顺序，以控制它们的外观在模板类别树中。

 由于其设计 **，VSTemplateDir** 条目应仅出现在非区域设置指定的清单中。

### <a name="attributes"></a>特性
 无。

### <a name="child-elements"></a>子元素

- **RelativePath：** 模板的路径。 每个路径只能有一个条目，因此第一个条目将赢得所有清单。

- **LocalizedName：** 指定本地化名称的 **NameDescriptionIcon** 元素。 可选。

- **SortOrder：** 指定排序顺序的字符串。 可选。

- **ParentFolderOverrideName：** 父文件夹的重写名称。 可选。 此元素具有 **Name** 属性，它是指定名称的字符串值。

### <a name="parent-element"></a>父元素
 **VSTemplateManifest**

## <a name="namedescriptionicon"></a>NameDescriptionIcon
 指定可能用于本地化模板的名称和说明。 请参阅 **上面的 LocalizedName。**

### <a name="attributes"></a>特性

- **包**：指定包的字符串值。 可选。

- **ID：** 指定 ID 的字符串值。 可选。

### <a name="child-elements"></a>子元素
 无。

### <a name="parent-element"></a>父元素
 **LocalizedName**

## <a name="examples"></a>示例
 以下代码是项目模板 *.vstman 文件* 的示例。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\TestProjectTemplate</RelativePathOnDisk>
    <TemplateFileName>TestProjectTemplate.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>TestProjectTemplate</Name>
        <Description>TestProjectTemplate</Description>
        <Icon>TestProjectTemplate.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>aac0aeea-7883-4003-992f-937d53d70ab1</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>TestProjectTemplate</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 以下代码是项模板 *.vstman 文件* 的示例。

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Item">
    <RelativePathOnDisk>CSharp\1033\ItemTemplate1</RelativePathOnDisk>
    <TemplateFileName>ItemTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ItemTemplate1</Name>
        <Description>ItemTemplate1</Description>
        <Icon>ItemTemplate1.ico</Icon>
        <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
        <DefaultName>Class.cs</DefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```
