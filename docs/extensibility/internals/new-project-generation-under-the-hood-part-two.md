---
title: 新Project代：在底层，第二部分|Microsoft Docs
description: 详细了解在 IDE Visual Studio 集成开发环境中会发生什么 (IDE) 创建你自己的项目类型 (第 2 部分（第 2 部分) ）。
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio], new project dialog
- projects [Visual Studio], new project generation
ms.assetid: 73ce91d8-0ab1-4a1f-bf12-4d3c49c01e13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 77ee63fbc49554ad3d9037f7d5bf3d19e4cf29f16ec43d384a0489da9ec06184
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432342"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>生成新项目：揭秘，第 2 部分

在 ["Project](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)代：第一部分"中，我们看到了"新建 **Project对话框的** 填充。 假设你已选择 Visual **C#** Windows应用程序，填写了"名称"和"位置"文本框，并单击了"确定"。

## <a name="generating-the-solution-files"></a>生成解决方案文件
 选择应用程序模板将指示解压缩并打开相应的 .vstemplate 文件，并启动模板以解释 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 此文件中的 XML 命令。 这些命令将创建新解决方案或现有解决方案中的项目和项目项。

 该模板从保存 .vstemplate 文件的同一.zip文件夹解压缩名为项模板的源文件。 模板将这些文件复制到新项目，并相应地进行自定义。

### <a name="template-parameter-replacement"></a>模板参数替换
 当模板将项模板复制到新项目时，它会将任何模板参数替换为字符串来自定义文件。 模板参数是一种特殊令牌，前面后跟一个美元符号，例如，$date$。

 让我们看看典型的项目项模板。 提取并检查 Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 中的 Program.cs。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace $safeprojectname$
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

如果为名为 Simple Windows应用程序项目创建新的参数，则模板将 参数 `$safeprojectname$` 替换为项目的名称。

```csharp
using System;
using System.Collections.Generic;
using System.Windows.Forms;

namespace Simple
{
    static class Program
    {
        // source code deleted here for brevity
    }
}
```

 有关模板参数的完整列表，请参阅 [模板参数](../../ide/template-parameters.md)。

## <a name="a-look-inside-a-vstemplate-file"></a>在 中查找 。VSTemplate 文件
 基本 .vstemplate 文件采用此格式

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 我们查看了"新一代：Project第一部分"中的 \<TemplateData> [部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)。 本部分中的标记用于控制"新建 **Project的外观。**

 节中的 \<TemplateContent> 标记控制新项目和项目项的生成。 下面是 \<TemplateContent> \Program Files\Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中 cswindowsapplication.vstemplate 文件的 部分。

```xml
<TemplateContent>
  <Project File="WindowsApplication.csproj" ReplaceParameters="true">
    <ProjectItem ReplaceParameters="true"
      TargetFileName="Properties\AssemblyInfo.cs">
      AssemblyInfo.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Resources.resx">
      Resources.resx
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Resources.Designer.cs">
      Resources.Designer.cs
    </ProjectItem>
    <ProjectItem TargetFileName="Properties\Settings.settings">
      Settings.settings
    </ProjectItem>
    <ProjectItem ReplaceParameters="true"       TargetFileName="Properties\Settings.Designer.cs">
      Settings.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true" OpenInEditor="true">
      Form1.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Form1.Designer.cs
    </ProjectItem>
    <ProjectItem ReplaceParameters="true">
      Program.cs
    </ProjectItem>
  </Project>
</TemplateContent>
```

 \<Project>标记控制项目的生成，标记控制 \<ProjectItem> 项目项的生成。 如果参数 ReplaceParameters 为 true，则模板将自定义项目文件或项中的所有模板参数。 在这种情况下，除 设置.settings 外，所有项目项都是自定义的。

 TargetFileName 参数指定生成的项目文件或项的名称和相对路径。 这样，你可以为项目创建文件夹结构。 如果不指定此参数，则项目项将具有与项目项模板相同的名称。

 生成的Windows文件夹结构如下所示：

 ![屏幕截图显示了Windows"简单"解决方案的应用程序文件夹Visual Studio 解决方案资源管理器。](../../extensibility/internals/media/simplesolution.png)

 模板中的第 \<Project> 一个和唯一标记显示为：

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 这会指示 New Project 模板通过复制和自定义模板项 windowsapplication.csproj 来创建 Simple.csproj 项目文件。

### <a name="designers-and-references"></a>设计器和引用
 可以在"属性"解决方案资源管理器"属性"文件夹存在并包含预期文件。 但是，项目引用和设计器文件依赖项（例如 Resources.Designer.cs 到 Resources.resx 和 Form1.Designer.cs 到 Form1.cs）呢？  这些是在生成 Simple.csproj 文件时在文件中设置的。

 下面是 \<ItemGroup> Simple.csproj 中用于创建项目引用的 ：

```xml
<ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Data" />
    <Reference Include="System.Deployment" />
    <Reference Include="System.Drawing" />
    <Reference Include="System.Windows.Forms" />
    <Reference Include="System.Xml" />
</ItemGroup>
```

 可以看到，这些引用是项目名称中的六个项目解决方案资源管理器。 下面是另一部分 \<ItemGroup> 。 为清楚起见，删除了许多代码行。 本部分介绍设置。依赖于 设置.settings 的 Designer.cs：

```xml
<ItemGroup>
    <Compile Include="Properties\Settings.Designer.cs">
        <DependentUpon>Settings.settings</DependentUpon>
    </Compile>
</ItemGroup>
```

## <a name="see-also"></a>另请参阅

- [生成新项目：揭秘，第 1 部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)
- [MSBuild](../../msbuild/msbuild.md)
