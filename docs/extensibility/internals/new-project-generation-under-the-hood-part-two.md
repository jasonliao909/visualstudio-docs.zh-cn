---
title: 新 Project 生成：在后台，第二部分 |Microsoft Docs
description: 请详细了解 Visual Studio 集成开发环境中发生的情况 (IDE) 创建自己的项目类型 (第2部分（共) 2 部分）。
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
ms.openlocfilehash: 56e1fa13846525221ec96dca3a8b744590e1dc8d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600712"
---
# <a name="new-project-generation-under-the-hood-part-two"></a>生成新项目：揭秘，第 2 部分

在 [新的 Project 代中：](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)在幕后，我们看到了一个 "**新 Project** " 对话框的填充方式。 假设您已经选择了 **Visual c # Windows 应用程序**，填充了 "**名称**" 和 "**位置**" 文本框，然后单击 "确定"。

## <a name="generating-the-solution-files"></a>生成解决方案文件
 选择应用程序模板 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 将指示解压缩并打开相应的 .vstemplate 文件，并启动一个模板来解释此文件中的 XML 命令。 这些命令在新的或现有的解决方案中创建项目和项目项。

 包含 .vstemplate 文件的同一个 .zip 文件夹中名为项模板的模板解压缩源文件。 模板将这些文件复制到新项目，并相应地对其进行自定义。

### <a name="template-parameter-replacement"></a>模板参数替换
 当模板将项模板复制到新的项目时，它会将任何模板参数替换为字符串，以自定义该文件。 模板参数是一种特殊的标记，该标记前面和后面跟有美元符号，例如 $date $。

 让我们看一看典型的项目项模板。 在 program Files \ Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中提取并检查 program。

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

如果创建名为 Simple 的新 Windows 应用程序项目，则模板会将参数替换为 `$safeprojectname$` 项目的名称。

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

## <a name="a-look-inside-a-vstemplate-file"></a>中的外观。.Vstemplate 文件
 基本的 .vstemplate 文件具有此格式

```xml
<VSTemplate Version="2.0.0"     xmlns="http://schemas.microsoft.com/developer/vstemplate/2005"     Type="Project">
    <TemplateData>
    </TemplateData>
    <TemplateContent>
    </TemplateContent>
</VSTemplate>
```

 我们在新的 \<TemplateData> Project 代中查看了一节[：在幕后，第一部分](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)。 本节中的标记用于控制 **新 Project** 对话框的外观。

 部分中的标记 \<TemplateContent> 控制新项目和项目项的生成。 下面是 \<TemplateContent> cswindowsapplication 文件中的部分，位于 \Program Files \ Microsoft Visual Studio 8\Common7\IDE\ProjectTemplates\CSharp\Windows\1033\WindowsApplication.zip 文件夹中。

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

 \<Project>标记控制项目的生成， \<ProjectItem> 标记控制项目项的生成。 如果参数 ReplaceParameters 为 true，则模板将自定义项目文件或项中的所有模板参数。 在这种情况下，将自定义所有项目项，设置设置除外。

 TargetFileName 参数指定生成的项目文件或项的名称和相对路径。 这使你可以为项目创建文件夹结构。 如果未指定此参数，则项目项的名称将与项目项模板的名称相同。

 生成的 Windows 应用程序文件夹结构如下所示：

 ![Visual Studio 解决方案资源管理器中 "简单" 解决方案的 Windows 应用程序文件夹结构的屏幕截图。](../../extensibility/internals/media/simplesolution.png)

 模板中的第一个和唯一的 \<Project> 标记将读取：

```xml
<Project File="WindowsApplication.csproj" ReplaceParameters="true">
```

 这会指示新的 Project 模板通过复制并自定义模板项 windowsapplication.zip 来创建简单的 .csproj 项目文件。

### <a name="designers-and-references"></a>设计器和引用
 可以在解决方案资源管理器中看到 "属性" 文件夹存在并且包含所需的文件。 但对于项目引用和设计器文件依赖项（如 node.js）以及从 .cs 到 Form1 的 .cs，会怎么样？  它们是在生成时在简单的 .csproj 文件中设置的。

 下面是 \<ItemGroup> 从简单的 .csproj 创建项目引用：

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

 您可以看到，这是解决方案资源管理器中显示的六个项目引用。 下面是另一个部分 \<ItemGroup> 。 为清楚起见，已经删除了许多代码行。 本部分进行设置。与设置相关的设计器。设置：

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
