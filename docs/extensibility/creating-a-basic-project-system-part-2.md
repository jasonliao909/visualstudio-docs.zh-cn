---
title: 创建基本Project系统，第 2 部分|Microsoft Docs
description: 了解如何将Visual Studio模板、属性页和其他功能添加到上一篇文章中创建的项目。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: aee48fc6-a15f-4fd5-8420-7f18824de220
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 644921dac3a82da3ad618eda8787ee6866689753696268d026e73955ae286078
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452697"
---
# <a name="create-a-basic-project-system-part-2"></a>创建基本项目系统，第 2 部分
本系列的第一个演练（创建基本项目系统，第 [1](../extensibility/creating-a-basic-project-system-part-1.md)部分）演示如何创建基本项目系统。 本演练基于基本项目系统，Visual Studio模板、属性页和其他功能。 在开始本演练之前，必须完成第一个演练。

本演练将指导如何创建项目文件扩展名 *为 .myproj 的项目类型*。 若要完成本演练，不需要创建自己的语言，因为本演练借用了现有的 Visual C# 项目系统。

本演练将指导如何完成以下任务：

- 创建Visual Studio模板。

- 部署Visual Studio模板。

- 在"新建项目"对话框中创建项目 **Project节点。**

- 在模板中启用Visual Studio替换。

- 创建项目属性页。

> [!NOTE]
> 本演练中的步骤基于 C# 项目。 但是，除了文件扩展名和代码等特定内容外，还可以对项目使用Visual Basic步骤。

## <a name="create-a-visual-studio-template"></a>创建Visual Studio模板
- [创建基本项目系统，第 1](../extensibility/creating-a-basic-project-system-part-1.md) 部分演示如何创建基本项目模板并将其添加到项目系统。 它还演示如何使用 属性向 Visual Studio注册此模板，该属性在系统注册表中写入 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> *\\ Templates\Projects\SimpleProject \\* 文件夹的完整路径。

通过使用 Visual Studio模板 (*.vstemplate* 文件) 而不是基本项目模板，可以控制模板在"新建 **Project"** 对话框中的显示方式以及模板参数的替换方式。 *.vstemplate* 文件是一个 XML 文件，描述在使用项目系统模板创建项目时如何包括源文件。 项目系统本身通过收集 *.vstemplate* 文件和 *.zip* 文件中源文件来生成，并且通过将 *.zip* 文件复制到已知位置进行部署Visual Studio。 本演练稍后将更详细地介绍此过程。

1. 在 中，打开按照创建基本项目系统第 1 部分创建 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] [的简单项目解决方案](../extensibility/creating-a-basic-project-system-part-1.md)。

2. 在 *SimpleProjectPackage.cs* 文件中，找到 ProvideProjectFactory 属性。 将项目名称 (参数替换为 null) ，将第四个参数替换为 ("作为项目模板文件夹) 路径。 \\\NullPath"，如下所示。

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. 将名为 *SimpleProject.vstemplate* 的 XML 文件添加到 *\\ Templates\Projects\SimpleProject \\* 文件夹。

4. 将 *SimpleProject.vstemplate* 的内容替换为以下代码。

    ```xml
    <VSTemplate Version="2.0.0" Type="Project"
        xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
      <TemplateData>
        <Name>SimpleProject Application</Name>
        <Description>
          A project for creating a SimpleProject application
        </Description>
        <Icon>SimpleProject.ico</Icon>
        <ProjectType>SimpleProject</ProjectType>
      </TemplateData>
      <TemplateContent>
        <Project File="SimpleProject.myproj" ReplaceParameters="true">
          <ProjectItem ReplaceParameters="true" OpenInEditor="true">
            Program.cs
          </ProjectItem>
          <ProjectItem ReplaceParameters="true" OpenInEditor="false">
            AssemblyInfo.cs
          </ProjectItem>
        </Project>
      </TemplateContent>
    </VSTemplate>
    ```

5. 在"**属性"** 窗口中，选择 *\\ Templates\Projects\SimpleProject \\* 文件夹中的所有五个文件，将"生成 **操作**"设置为 **ZipProject**。

    ![简单Project文件夹](../extensibility/media/simpproj2.png "SimpProj2")

    \<TemplateData>部分确定"新建项目"对话框中 SimpleProject 项目Project和外观，如下所示：

- 元素 \<Name> 将项目模板命名为 SimpleProject 应用程序。

- 元素 \<Description> 包含选择项目模板时"新建Project对话框中显示的说明。

- 元素 \<Icon> 指定与 SimpleProject 项目类型一起出现的图标。

- 元素 \<ProjectType> 在"新建Project"对话框中将Project类型。 此名称替换 ProvideProjectFactory 属性的项目名称参数。

  > [!NOTE]
  > \<ProjectType>元素必须与 `LanguageVsTemplate` `ProvideProjectFactory` SimpleProjectPackage.cs 文件中 特性的 参数匹配。

  \<TemplateContent>部分介绍创建新项目时生成的这些文件：

- *SimpleProject.myproj*

- *Program.cs*

- *AssemblyInfo.cs*

  所有三个文件 `ReplaceParameters` 都设置为 true，这将启用参数替换。 *Program.cs* 文件已设置为 true，这会导致创建项目时在代码 `OpenInEditor` 编辑器中打开该文件。

  有关模板架构中的元素Visual Studio，请参阅模板Visual Studio[架构引用](../extensibility/visual-studio-template-schema-reference.md)。

> [!NOTE]
> 如果一个项目具有多个Visual Studio模板，则每个模板都位于单独的文件夹中。 该文件夹中每个文件都必须将"**生成操作**"设置为 **"ZipProject"。**

## <a name="adding-a-minimal-vsct-file"></a>添加最小的 .vsct 文件
 Visual Studio必须在安装模式下运行，以识别新模板或修改Visual Studio模板。 安装模式要求 *存在 .vsct* 文件。 因此，必须将最小的 *.vsct* 文件添加到项目。

1. 将名为 *SimpleProject.vsct* 的 XML 文件添加到 SimpleProject 项目。

2. 将 *SimpleProject.vsct* 文件的内容替换为以下代码。

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. 将 **此文件的生成** 操作设置为 **VSCTCompile**。 只能在 *.csproj* 文件中执行此操作，而不是在"属性 **"窗口中** 这样做。 此时， **请确保此文件** 的"生成操作"设置为 **"无** "。

    1. 右键单击 SimpleProject 节点，然后单击"**编辑 SimpleProject.csproj"。**

    2. 在 *.csproj* 文件中，找到 *SimpleProject.vsct* 项。

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. 将生成操作更改为 **VSCTCompile**。

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. 项目文件并关闭编辑器。

    5. 保存 SimpleProject 节点，然后在 **解决方案资源管理器重载****Project。**

## <a name="examine-the-visual-studio-template-build-steps"></a>检查Visual Studio模板生成步骤
 当更改 *.vstemplate* 文件或重新生成包含 *.vstemplate* 文件的项目时，VSPackage 项目生成系统Visual Studio在安装模式下运行。 可以按照以下方法操作：将属性的MSBuild级别设置为"正常"或更高。

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 展开"**项目和解决方案"节点**，然后选择"生成 **并运行"。**

3. 将 **MSBuild生成输出详细级别设置为****"正常"。** 单击“确定”。

4. 重新生成 SimpleProject 项目。

    创建项目文件的 *.zip步骤应* 类似于以下示例。

```
ZipProjects:
1>  Zipping ProjectTemplates
1>  Zipping <path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip...
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "<%LOCALAPPDATA%>\Microsoft\VisualStudio\14.0Exp\ProjectTemplates\\\\SimpleProject.zip".
1>  Copying file from "<path>\SimpleProject\SimpleProject\obj\Debug\SimpleProject.zip" to "bin\Debug\\ProjectTemplates\\\\SimpleProject.zip".
1>  SimpleProject -> <path>\SimpleProject\SimpleProject\bin\Debug\ProjectTemplates\SimpleProject.zip
1>ZipItems:
1>  Zipping ItemTemplates
1>  SimpleProject ->
```

## <a name="deploy-a-visual-studio-template"></a>部署Visual Studio模板
Visual Studio模板不包含路径信息。 因此 *，.zip* 模板文件必须部署到已知Visual Studio。 ProjectTemplates 文件夹的位置通常为 *<%LOCALAPPDATA%>\Microsoft\VisualStudio\14.0Exp\ProjectTemplates*。

若要部署项目工厂，安装程序必须具有管理员权限。 它将模板部署在 Visual Studio 节点下 *：...\Microsoft Visual Studio 14.0\Common7\IDE\ProjectTemplates*。

## <a name="test-a-visual-studio-template"></a>测试Visual Studio模板
测试项目工厂，看它是否使用项目模板创建Visual Studio层次结构。

1. 重置 Visual Studio SDK 实验实例。

    在 [!INCLUDE[win7](../debugger/includes/win7_md.md)] 上：在"开始"菜单上，找到 **"Microsoft Visual Studio/Microsoft Visual Studio SDK/Tools"** 文件夹，然后选择"重置Microsoft Visual Studio **实验实例"。**

    在更高版本的 Windows：**在"开始**"屏幕上，键入"重置Microsoft Visual Studio **\<version> 实验实例"。**

2. 将出现命令提示符窗口。 看到"按任意 **键继续"字样时，单击**"**输入"。** 窗口关闭后，打开Visual Studio。

3. 重新生成 SimpleProject 项目并开始调试。 这将显示实验实例。

4. 在实验实例中，创建 SimpleProject 项目。 在"**新建Project** 对话框中，选择"**简单""项目"。**

5. 应会看到 SimpleProject 的新实例。

    ![简单Project新实例](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![我的Project新实例](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>创建项目类型子节点
可以在"新建项目"对话框中将子节点添加到 **Project节点。** 例如，对于 SimpleProject 项目类型，可以具有控制台应用程序、窗口应用程序、Web 应用程序等的子节点。

子节点通过更改项目文件并添加到元素 \<OutputSubPath> 中创建 \<ZipProject> 。 在生成或部署期间复制模板时，每个子节点将成为项目模板文件夹的子文件夹。

本部分演示如何为 SimpleProject 项目类型创建控制台子节点。

1. 将 *\\ Templates\Projects\SimpleProject \\* 文件夹重命名为 *\\ Templates\Projects\ConsoleApp \\*。

2. 在"**属性"** 窗口中，选择 *\\ Templates\Projects\ConsoleApp \\* 文件夹中的所有五个文件，并确保"生成操作 **"设置为** **ZipProject**。

3. 在 SimpleProject.vstemplate 文件中，在 节末尾的 结束标记之前添加 \<TemplateData> 以下行。

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    这将导致控制台应用程序模板同时显示在控制台子节点和 SimpleProject 父节点中，该父节点位于子节点上方的一个级别。

4. 保存 *SimpleProject* 文件。

5. 在 *.csproj* 文件中，将添加 \<OutputSubPath> 到每个 ZipProject 元素。 像以前一样卸载项目，然后编辑项目文件。

6. 找到 \<ZipProject> 元素。 对于每个 \<ZipProject> 元素，添加一个 \<OutputSubPath> 元素并为其指定值控制台。 ZipProject

    ```
    <ZipProject Include="Templates\Projects\ConsoleApp\AssemblyInfo.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\Program.cs">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.myproj">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.vstemplate">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    <ZipProject Include="Templates\Projects\ConsoleApp\SimpleProject.ico">
      <OutputSubPath>Console</OutputSubPath>
    </ZipProject>
    ```

7. 将以下 \<PropertyGroup> 内容添加到项目文件：

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. 保存项目文件，然后重新加载项目。

## <a name="test-the-project-type-child-node"></a>测试项目类型子节点
测试修改后的项目文件，以查看 "**新建 Project** " 对话框中是否显示了 **控制台** 子节点。

1. 运行 "**重置 Microsoft Visual Studio 实验实例**" 工具。

2. 重新生成 SimpleProject 项目并开始调试。 应显示实验实例

3. 在 "**新建 Project** " 对话框中，单击 " **SimpleProject** " 节点。 " **控制台应用程序** " 模板应出现在 " **模板** " 窗格中。

4. 展开 " **SimpleProject** " 节点。 **控制台** 子节点应会出现。 " **SimpleProject" 应用程序** 模板将继续出现在 " **模板** " 窗格中。

5. 单击 " **取消** " 和 "停止调试"。

    ![简单 Project 汇总](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![简单 Project 控制台节点](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>替换项目模板参数
- [创建基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md) 演示了如何覆盖 `ProjectNode.AddFileFromTemplate` 方法，以执行基本类型的模板参数替换。 本部分介绍如何使用更复杂的 Visual Studio 模板参数。

使用 "**新建 Project** " 对话框中的 Visual Studio 模板创建项目时，模板参数将替换为字符串以自定义项目。 模板参数是以美元符号开头和结尾的特殊标记，例如 $time $。 以下两个参数对于启用基于模板的项目中的自定义特别有用：

- $GUID [1-10] $ 替换为新的 Guid。 最多可以指定10个唯一的 Guid，例如 $guid $1。

- $safeprojectname $ 是用户在 "**新建 Project** " 对话框中提供的名称，则将其修改为删除所有不安全字符和空格。

  有关模板参数的完整列表，请参阅[模板参数](../ide/template-parameters.md)。

### <a name="to-substitute-project-template-parameters"></a>替换项目模板参数

1. 在 *SimpleProjectNode* 文件中，删除 `AddFileFromTemplate` 方法。

2. 在 *\\ Templates\Projects\ConsoleApp\SimpleProject.myproj* 文件中，找到 \<RootNamespace> 属性，并将其值更改为 $safeprojectname $。

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. 在 *\\ Templates\Projects\SimpleProject\Program.cs* 文件中，将该文件的内容替换为以下代码：

    ```
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace $safeprojectname$
    {
        [Guid("$guid1$")]
        public class $safeprojectname$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

4. 重新生成 SimpleProject 项目并开始调试。 应显示实验实例。

5. 创建新的 SimpleProject 控制台应用程序。  (在 " **Project 类型**" 窗格中，选择 " **SimpleProject**"。 在 **Visual Studio 安装的模板**"下，选择"**控制台应用程序**"。 ) 

6. 在新创建的项目中，打开 " *.cs*"。 其外观应如下所示 (文件中的 GUID 值会有所不同。 ) ：

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;
    using System.Runtime.InteropServices;    // Guid

    namespace Console_Application1
    {
        [Guid("00000000-0000-0000-00000000-00000000)"]
        public class Console_Application1
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

## <a name="create-a-project-property-page"></a>创建项目属性页
您可以为您的项目类型创建属性页，以便用户可以在基于模板的项目中查看和更改属性。 本部分说明如何创建独立于配置的属性页。 此基本属性页使用属性网格显示您在属性页类中公开的公共属性。

从基类派生属性页类 `SettingsPage` 。 类提供的 "属性" 网格 `SettingsPage` 可识别大多数基元数据类型，并知道如何显示它们。 此外，类还 `SettingsPage` 知道如何将属性值保存到项目文件。

您在本部分中创建的属性页使您可以更改和保存这些项目属性：

- AssemblyName

- OutputType

- RootNamespace.

1. 在 *SimpleProjectPackage* 文件中，将以下属性添加 `ProvideObject` 到 `SimpleProjectPackage` 类：

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    这会向 COM 注册属性页类 `GeneralPropertyPage` 。

2. 在 *SimpleProjectNode* 文件中，将以下两个重写方法添加到 `SimpleProjectNode` 类：

    ```csharp
    protected override Guid[] GetConfigurationIndependentPropertyPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    protected override Guid[] GetPriorityProjectDesignerPages()
    {
        Guid[] result = new Guid[1];
        result[0] = typeof(GeneralPropertyPage).GUID;
        return result;
    }
    ```

    这两种方法都返回属性页 Guid 的数组。 GeneralPropertyPage GUID 是数组中的唯一元素，因此，" **属性页** " 对话框将只显示一页。

3. 将名为 *GeneralPropertyPage* 的类文件添加到 SimpleProject 项目。

4. 使用以下代码替换该文件的内容：

    ```csharp
    using System;
    using System.Runtime.InteropServices;
    using Microsoft.VisualStudio;
    using Microsoft.VisualStudio.Project;
    using System.ComponentModel;

    namespace SimpleProject
    {
        [ComVisible(true)]
        [Guid("6BC7046B-B110-40d8-9F23-34263D8D2936")]
        public class GeneralPropertyPage : SettingsPage
        {
            private string assemblyName;
            private OutputType outputType;
            private string defaultNamespace;

            public GeneralPropertyPage()
            {
                this.Name = "General";
            }

            [Category("AssemblyName")]
            [DisplayName("AssemblyName")]
            [Description("The output file holding assembly metadata.")]
            public string AssemblyName
            {
                get { return this.assemblyName; }
            }
            [Category("Application")]
            [DisplayName("OutputType")]
            [Description("The type of application to build.")]
            public OutputType OutputType
            {
                get { return this.outputType; }
                set { this.outputType = value; this.IsDirty = true; }
            }
            [Category("Application")]
            [DisplayName("DefaultNamespace")]
            [Description("Specifies the default namespace for added items.")]
            public string DefaultNamespace
            {
                get { return this.defaultNamespace; }
                set { this.defaultNamespace = value; this.IsDirty = true; }
            }

            protected override void BindProperties()
            {
                this.assemblyName = this.ProjectMgr.GetProjectProperty("AssemblyName", true);
                this.defaultNamespace = this.ProjectMgr.GetProjectProperty("RootNamespace", false);

                string outputType = this.ProjectMgr.GetProjectProperty("OutputType", false);
                this.outputType = (OutputType)Enum.Parse(typeof(OutputType), outputType);
            }

            protected override int ApplyChanges()
            {
                this.ProjectMgr.SetProjectProperty("AssemblyName", this.assemblyName);
                this.ProjectMgr.SetProjectProperty("OutputType", this.outputType.ToString());
                this.ProjectMgr.SetProjectProperty("RootNamespace", this.defaultNamespace);
                this.IsDirty = false;

                return VSConstants.S_OK;
            }
        }
    }
    ```

    `GeneralPropertyPage`类公开三个公共属性 AssemblyName、OutputType 和 RootNamespace。 由于 AssemblyName 没有 set 方法，因此它显示为只读属性。 OutputType 是一个枚举常数，因此它显示为下拉列表。

    `SettingsPage`提供基类 `ProjectMgr` 以保持属性。 `BindProperties`方法使用 `ProjectMgr` 检索持久化属性值并设置相应的属性。 `ApplyChanges`方法使用 `ProjectMgr` 获取属性的值，并将这些值保存到项目文件。 属性 set 方法将设置 `IsDirty` 为 true，以指示必须保存属性。 保存项目或解决方案时，将发生持久性。

5. 重新生成 SimpleProject 解决方案并启动调试。 应显示实验实例。

6. 在实验实例中，创建一个新的 SimpleProject 应用程序。

7. Visual Studio 通过使用 Visual Studio 模板来调用项目工厂来创建项目。 新的 *Program .cs* 文件将在代码编辑器中打开。

8. 右键单击 " **解决方案资源管理器** 中的项目节点，然后单击" **属性**"。 随即显示“属性页”对话框。

    ![简单 Project 属性页](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>测试项目属性页
现在，你可以测试是否可以修改和更改属性值。

1. 在 " **MyConsoleApplication 属性页** " 对话框中，将 " **DefaultNamespace** " 更改为 " **MyApplication**"。

2. 选择 " **OutputType** " 属性，然后选择 **"类库"。**

3. 单击“应用”，然后单击“确定”。

4. 重新打开 " **属性页** " 对话框，并验证所做的更改是否已保存。

5. 关闭 Visual Studio 的实验实例。

6. 重新打开实验实例。

7. 重新打开 " **属性页** " 对话框，并验证所做的更改是否已保存。

8. 关闭 Visual Studio 的实验实例。
    ![关闭实验实例](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
