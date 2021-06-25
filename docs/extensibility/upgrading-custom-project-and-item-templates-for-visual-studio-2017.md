---
title: 升级 2017 Visual Studio的自定义项目和项模板
titleSuffix: ''
description: 了解如何从早期版本的 Visual Studio SDK 更新自定义项目和项模板，Visual Studio 2017 及更高版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: ad02477b-e101-4f32-aeb7-292bf95d5c2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 0d07af0a00ab840df8a9af437bcddc427f606948
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903055"
---
# <a name="upgrade-custom-project-and-item-templates-for-visual-studio-2017"></a>升级自定义Visual Studio 项目和项模板 2017

从 Visual Studio 2017 Visual Studio 开始，Visual Studio 以不同于以前版本的 Visual Studio 的方式发现 .vsix 或 .msi 安装的项目和项模板。 如果你拥有使用自定义项目或项模板的扩展，则需要更新扩展。 本文介绍必须执行哪些工作。

此更改仅影响 Visual Studio 2017 年。 它不会影响早期版本的 Visual Studio。

如果要创建项目或项模板作为 VSIX 扩展的一部分，请参阅 [创建自定义项目和项模板](../extensibility/creating-custom-project-and-item-templates.md)。

## <a name="template-scanning"></a>模板扫描

在早期版本的 Visual Studio 中 **，devenv /setup** 或 **devenv /installvstemplates** 扫描了本地磁盘以查找项目和项模板。 从 2017 Visual Studio开始，仅针对用户级别位置执行扫描。 默认用户级别位置为 **%USERPROFILE%\Documents \\<Visual Studio \> \Templates \\**。 如果在向导中选择了"自动将模板导入Visual Studio"选项，则此位置用于"项目导出模板  >  **..."命令生成的** 模板。

对于 (非用户) ，必须包含一个清单 (.vstman) 文件，该文件指定模板的位置和其他特征。 .vstman 文件与用于模板的 .vstemplate 文件一起生成。 如果使用 .vsix 安装扩展，可以通过在 2017 年 1 月重新编译扩展Visual Studio完成此操作。 但是，如果使用 .msi，则需要手动进行更改。 有关进行这些更改需要执行哪些工作的列表，请参阅本页.MSI安装的扩展升级。

## <a name="how-to-update-a-vsix-extension-with-project-or-item-templates"></a>如何使用项目或项模板更新 VSIX 扩展

1. 在 2017 Visual Studio中打开解决方案。 将要求你升级代码。 单击“确定”。

2. 升级完成后，可能需要更改安装目标的版本。 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件并选择"**安装目标"** 选项卡。如果"**版本范围"** 字段 **为 [14.0]，** 请单击"编辑"，并更改该字段以Visual Studio 2017。  例如，可以将其设置为 **[14.0，15.0]，** 以将扩展安装到 Visual Studio 2015 或 Visual Studio 2017，或设置为 **[15.0]** 以将其安装到 Visual Studio 2017。

3. 重新编译代码。

4. 关闭 Visual Studio。

5. 安装 VSIX。

6. 可以通过执行以下操作来测试更新：

    1. 文件扫描更改由以下注册表项激活：

         **reg add hklm\software\microsoft\visualstudio\15.0\VSTemplate /v DisableTemplateScanning /t REG_DWORD /d 1 /reg：32**

    2. 添加密钥后，运行 **devenv /installvstemplates**。

    3. 重新打开Visual Studio。 应在预期位置找到模板。

    > [!NOTE]
    > 当Visual Studio存在时，扩展性项目模板不可用。 必须删除注册表项 (重新运行 **devenv /installvstemplates**) 以使用它们。

## <a name="other-recommendations-for-deploying-project-and-item-templates"></a>有关部署项目和项模板的其他建议

- 避免使用压缩的模板文件。 压缩的模板文件需要解压缩才能检索资源和内容，因此使用成本会更昂贵。 相反，应该将项目和项模板部署为其自己的目录中的单个文件，以加速模板初始化。 对于 VSIX 扩展，SDK 生成任务在创建 VSIX 文件时会自动解压缩任何压缩的模板。

- 避免将包/资源 ID 条目用于模板名称、说明、图标或预览，以避免在模板发现过程中加载不必要的资源程序集。 相反，可以使用本地化清单为每个区域设置创建模板项，该条目使用本地化的名称或属性。

- 如果将模板包括为文件项，则清单生成可能不会提供预期结果。 在这种情况下，你必须将手动生成的清单添加到 VSIX 项目。

## <a name="file-changes-in-project-and-item-templates"></a>项目和项模板中的文件更改
我们显示了模板文件的 Visual Studio 2015 Visual Studio 2017 版本之间的差异点，以便可以正确创建新文件。

 下面是 2015 年 1 月创建的默认Visual Studio .vstemplate 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Project" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ProjectTemplate1</Name>
    <Description>ProjectTemplate1</Description>
    <Icon>ProjectTemplate1.ico</Icon>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <SortOrder>1000</SortOrder>
    <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
    <CreateNewFolder>true</CreateNewFolder>
    <DefaultName>ProjectTemplate1</DefaultName>
    <ProvideDefaultName>true</ProvideDefaultName>
  </TemplateData>
  <TemplateContent>
    <Project File="ProjectTemplate.csproj" ReplaceParameters="true">
      <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
      <ProjectItem ReplaceParameters="true" OpenInEditor="true">Class1.cs</ProjectItem>
    </Project>
  </TemplateContent>
</VSTemplate>

```

 下面是 .vstman 文件 (可以在 VSIX 项目的清单目录中找到它) 重新生成 VSIX 项目的结果：

```xml
<VSTemplateManifest Version="1.0" Locale="1033" xmlns="http://schemas.microsoft.com/developer/vstemplatemanifest/2015">
  <VSTemplateContainer TemplateType="Project">
    <RelativePathOnDisk>CSharp\1033\ProjectTemplate1</RelativePathOnDisk>
    <TemplateFileName>ProjectTemplate1.vstemplate</TemplateFileName>
    <VSTemplateHeader>
      <TemplateData xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
        <Name>ProjectTemplate1</Name>
        <Description>ProjectTemplate1</Description>
        <Icon>ProjectTemplate1.ico</Icon>
        <ProjectType>CSharp</ProjectType>
        <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
        <SortOrder>1000</SortOrder>
        <TemplateID>05b79cc9-2146-4716-a8e5-7e085cdd2221</TemplateID>
        <CreateNewFolder>true</CreateNewFolder>
        <DefaultName>ProjectTemplate1</DefaultName>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
    </VSTemplateHeader>
  </VSTemplateContainer>
</VSTemplateManifest>

```

 [TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)元素提供的信息保持不变。 **\<VSTemplateContainer>** 元素指向关联模板的 .vstemplate 文件。

 下面是 2015 年 1 月创建的默认Visual Studio .vstemplate 文件：

```xml
<?xml version="1.0" encoding="utf-8"?>
<VSTemplate Version="3.0.0" Type="Item" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" xmlns:sdk="http://schemas.microsoft.com/developer/vstemplate-sdkextension/2010">
  <TemplateData>
    <Name>ItemTemplate1</Name>
    <Description>ItemTemplate1</Description>
    <Icon>ItemTemplate1.ico</Icon>
    <TemplateID>bfeadf8e-a251-4109-b605-516b88e38c8d</TemplateID>
    <ProjectType>CSharp</ProjectType>
    <RequiredFrameworkVersion>2.0</RequiredFrameworkVersion>
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    <DefaultName>Class.cs</DefaultName>
  </TemplateData>
  <TemplateContent>
    <References>
      <Reference>
        <Assembly>System</Assembly>
      </Reference>
    </References>
    <ProjectItem ReplaceParameters="true">Class.cs</ProjectItem>
  </TemplateContent>
</VSTemplate>

```

 下面是 .vstman 文件 (可以在 VSIX 项目的清单目录中找到它) 重新生成 VSIX 项目的结果：

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

 元素提供的信息 **\<TemplateData>** 保持不变。 **\<VSTemplateContainer>** 元素指向关联模板的 .vstemplate 文件

 有关 .vstman 文件的不同元素详细信息，请参阅Visual Studio [清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

## <a name="upgrades-for-extensions-installed-with-an-msi"></a>升级随应用程序一起安装的.MSI

某些基于 MSI 的扩展将模板部署到常见模板位置，如以下目录：

- **\<Visual Studio installation directory>\Common7\IDE \\<ProjectTemplates/ItemTemplates\>**

- **\<Visual Studio installation directory>\Common7\IDE\Extensions \\<ExtensionName \> \\<Project/ItemTemplates\>**

如果扩展执行基于 MSI 的部署，则需要手动生成模板清单，并确保该清单包含在扩展设置中。 比较上面列出的 .vstman 示例Visual Studio [模板清单架构参考](../extensibility/visual-studio-template-manifest-schema-reference.md)。

为项目和项模板创建单独的清单，它们应指向上面指定的根模板目录。 为每个扩展和区域设置创建一个清单。

## <a name="see-also"></a>另请参阅

- [模板发现疑难解答](troubleshooting-template-discovery.md)
- [创建自定义项目和项模板](creating-custom-project-and-item-templates.md)
