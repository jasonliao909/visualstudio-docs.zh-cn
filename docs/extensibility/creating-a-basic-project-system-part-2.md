---
title: 创建基本 Project 系统，第2部分 |Microsoft Docs
description: 了解如何向前面文章中创建的项目添加 Visual Studio 模板、属性页和其他功能。
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
ms.openlocfilehash: 4aa62227051b68307c0bb4ab301a218d8e535461
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600995"
---
# <a name="create-a-basic-project-system-part-2"></a>创建基本项目系统，第2部分
本系列中的第一个演练是 [创建一个基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md)显示了如何创建基本的项目系统。 本演练通过添加 Visual Studio 模板、属性页和其他功能来构建基本项目系统。 开始此演练之前，必须先完成第一个演练。

本演练讲授如何创建项目文件扩展名为 *myproj.csproj* 的项目类型。 若要完成本演练，您不必创建您自己的语言，因为该演练会从现有 Visual c # 项目系统中借用。

本演练介绍了如何完成以下任务：

- 创建 Visual Studio 模板。

- 部署 Visual Studio 模板。

- 在 "**新建 Project** " 对话框中创建项目类型子节点。

- 在 Visual Studio 模板中启用参数替换。

- 创建项目属性页。

> [!NOTE]
> 本演练中的步骤基于 c # 项目。 但是，除了文件扩展名和代码以外，你还可以对 Visual Basic 项目使用相同的步骤。

## <a name="create-a-visual-studio-template"></a>创建 Visual Studio 模板
- [创建基本项目系统，第1部分](../extensibility/creating-a-basic-project-system-part-1.md) 演示如何创建基本项目模板并将其添加到项目系统。 它还演示了如何使用特性将此模板注册到 Visual Studio <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> ，该属性将 *\\ Templates\Projects\SimpleProject \\* 文件夹的完整路径写入系统注册表中。

通过使用 Visual Studio 模板 (*.vstemplate* 文件) 而不是基本项目模板，可以控制模板在 "**新建 Project** " 对话框中的显示方式以及如何替换模板参数。 *.Vstemplate* 文件是一个 XML 文件，描述使用项目系统模板创建项目时如何包含源文件。 项目系统本身是通过收集 *.zip* 文件中的 *.vstemplate* 文件和源文件来构建的，并通过将 *.zip* 文件复制到 Visual Studio 已知的位置来进行部署。 本演练稍后将对此过程进行更详细的介绍。

1. 在中 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，打开通过 [创建基本项目系统（第1部分）](../extensibility/creating-a-basic-project-system-part-1.md)创建的 SimpleProject 解决方案。

2. 在 *SimpleProjectPackage* 文件中，找到 ProvideProjectFactory 属性。 将 (项目名称) 的第二个参数替换为 null，并将第四个参数 (项目模板文件夹的路径) 为 "。 \\\NullPath "，如下所示。

    ```
    [ProvideProjectFactory(typeof(SimpleProjectFactory), null,
        "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
        ".\\NullPath",
    LanguageVsTemplate = "SimpleProject")]
    ```

3. 将名为 *SimpleProject* 的 XML 文件添加到 *\\ Templates\Projects\SimpleProject \\* 文件夹。

4. 将 *SimpleProject* 的内容替换为以下代码。

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

5. 在 "**属性**" 窗口中，选择 *\\ Templates\Projects\SimpleProject \\* 文件夹中的所有五个文件，并将 "**生成操作**" 设置为 " **ZipProject**"。

    ![简单 Project 文件夹](../extensibility/media/simpproj2.png "SimpProj2")

    此 \<TemplateData> 部分确定 "**新建 Project** " 对话框中 "SimpleProject" 项目类型的位置和外观，如下所示：

- \<Name>元素命名要 SimpleProject 应用程序的项目模板。

- \<Description>元素包含的说明在选择项目模板时出现在 "**新建 Project** " 对话框中。

- \<Icon>元素指定与 SimpleProject 项目类型一起显示的图标。

- \<ProjectType>元素在 "**新建 Project** " 对话框中命名 Project 类型。 此名称替换 ProvideProjectFactory 属性的项目名称参数。

  > [!NOTE]
  > \<ProjectType>元素必须与 `LanguageVsTemplate` `ProvideProjectFactory` SimpleProjectPackage 文件中的属性的参数匹配。

  \<TemplateContent>部分介绍了在创建新项目时生成的这些文件：

- *SimpleProject. myproj.csproj*

- *Program.cs*

- *AssemblyInfo.cs*

  所有三个文件均 `ReplaceParameters` 设置为 true，这将启用参数替换。 *Program .cs* 文件已 `OpenInEditor` 设置为 true，这将导致在创建项目时在代码编辑器中打开该文件。

  有关 Visual Studio 模板架构中的元素的详细信息，请参阅[Visual Studio 模板架构参考](../extensibility/visual-studio-template-schema-reference.md)。

> [!NOTE]
> 如果项目有多个 Visual Studio 模板，则每个模板都在单独的文件夹中。 该文件夹中的每个文件都必须将 **生成操作** 设置为 **ZipProject**。

## <a name="adding-a-minimal-vsct-file"></a>添加最小的 .vsct 文件
 必须在安装模式下运行 Visual Studio 以识别新的或修改的 Visual Studio 模板。 安装模式要求存在 *.vsct* 文件。 因此，必须将最小的 *.vsct* 文件添加到项目。

1. 将名为 *SimpleProject. .vsct* 的 XML 文件添加到 SimpleProject 项目。

2. 将 *SimpleProject* 文件的内容替换为以下代码。

    ```
    <?xml version="1.0" encoding="utf-8" ?>
    <CommandTable
      xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable">
    </CommandTable>
    ```

3. 将此文件的 **生成操作** 设置为 **VSCTCompile**。 只能在 *.csproj* 文件中执行此操作，而不能在 " **属性** " 窗口中执行此操作。 请确保此时此文件的 **生成操作** 设置为 " **无** "。

    1. 右键单击 "SimpleProject" 节点，然后单击 " **编辑 SimpleProject**"。

    2. 在 *.csproj* 文件中，找到 " *SimpleProject. .vsct* " 项。

        ```
        <None Include="SimpleProject.vsct" />
        ```

    3. 将生成操作更改为 **VSCTCompile**。

        ```
        <VSCTCompile Include="SimpleProject.vsct" />
        ```

    4. 项目文件并关闭编辑器。

    5. 保存 "SimpleProject" 节点，然后在 "**解决方案资源管理器** 单击"**重载 "Project**。

## <a name="examine-the-visual-studio-template-build-steps"></a>检查 Visual Studio 模板生成步骤
 当更改 *.vstemplate* 文件或重新生成包含 *.vstemplate* 文件的项目时，VSPackage 项目生成系统通常会在安装模式下运行 Visual Studio。 可以通过将 MSBuild 的详细级别设置为 "正常" 或 "更高" 来执行此操作。

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 展开 " **项目和解决方案** " 节点，然后选择 " **生成并运行**"。

3. 将 **项目生成输出详细级别 MSBuild** 设置为 "**正常**"。 单击“确定”。

4. 重新生成 SimpleProject 项目。

    创建 *.zip* 项目文件的生成步骤应类似于以下示例。

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

## <a name="deploy-a-visual-studio-template"></a>部署 Visual Studio 模板
Visual Studio 模板不包含路径信息。 因此，模板 *.zip* 文件必须部署到 Visual Studio 已知的位置。 ProjectTemplates 文件夹的位置通常 *<% LOCALAPPDATA% > \microsoft\visualstudio\14.0exp\projecttemplates*。

若要部署项目工厂，安装程序必须具有管理员权限。 它在 Visual Studio 安装节点下部署模板： *... \ Microsoft Visual Studio 14.0 \ Common7\IDE\ProjectTemplates*。

## <a name="test-a-visual-studio-template"></a>测试 Visual Studio 模板
测试项目工厂，以查看它是否通过使用 Visual Studio 模板来创建项目层次结构。

1. 重置 Visual Studio SDK 实验实例。

    在上 [!INCLUDE[win7](../debugger/includes/win7_md.md)] ：在 "**开始**" 菜单上查找 **Microsoft Visual Studio/Microsoft Visual Studio SDK/Tools** 文件夹，然后选择 "**重置 Microsoft Visual Studio 实验实例"**。

    在的更高版本上 Windows：在 "**开始**" 屏幕上，键入 **"重置 Microsoft Visual Studio \<version> 实验实例"**。

2. 此时将显示命令提示符窗口。 看到字词 **按任意键继续** 时，单击 **enter**。 窗口关闭后，打开 Visual Studio。

3. 重新生成 SimpleProject 项目并开始调试。 这将显示实验实例。

4. 在实验实例中，创建一个 SimpleProject 项目。 在 "**新建 Project** " 对话框中，选择 " **SimpleProject**"。

5. 应会看到 SimpleProject 的新实例。

    ![简单 Project 新实例](../extensibility/media/simpproj2_newproj.png "SimpProj2_NewProj")

    ![我 Project 的新实例](../extensibility/media/simpproj2_myproj.png "SimpProj2_MyProj")

## <a name="create-a-project-type-child-node"></a>创建项目类型子节点
您可以在 "**新建 Project** " 对话框中将子节点添加到项目类型节点。 例如，对于 SimpleProject 项目类型，可以为控制台应用程序、窗口应用程序、web 应用程序等提供子节点。

通过更改项目文件并 \<OutputSubPath> 向元素添加子级来创建子节点 \<ZipProject> 。 在生成或部署过程中复制模板时，每个子节点都将成为 "项目模板" 文件夹的子文件夹。

本部分说明如何为 SimpleProject 项目类型创建控制台子节点。

1. 将 *\\ Templates\Projects\SimpleProject \\* 文件夹重命名为 *\\ Templates\Projects\ConsoleApp \\*。

2. 在 "**属性**" 窗口中，选择 *\\ Templates\Projects\ConsoleApp \\* 文件夹中的所有五个文件，并确保 "**生成操作**" 设置为 " **ZipProject**"。

3. 在 SimpleProject 文件中，将以下行添加到部分末尾的结束 \<TemplateData> 标记之前。

    ```
    <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
    ```

    这会导致 "控制台应用程序" 模板同时出现在控制台子节点和 "SimpleProject" 父节点中，这是子节点上的一个级别。

4. 保存 *SimpleProject.vstemplate* 文件。

5. 在 *.csproj* 文件中，将 \<OutputSubPath> 添加到每个 ZipProject 元素。 像以前一样卸载项目，并编辑项目文件。

6. 找到 \<ZipProject> 元素。 对于每个 \<ZipProject> 元素，请添加 \<OutputSubPath> 一个元素，并赋予其值 Console。 The ZipProject

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

7. 将此 \<PropertyGroup> 添加到项目文件：

    ```
    <PropertyGroup>
      <VsTemplateLanguage>SimpleProject</VsTemplateLanguage>
    </PropertyGroup>
    ```

8. 保存项目文件并重新加载项目。

## <a name="test-the-project-type-child-node"></a>测试项目类型子节点
测试修改后的项目文件，查看 **控制台子节点** 是否显示在"新建 **Project对话框中。**

1. 运行"**重置Microsoft Visual Studio实例"** 工具。

2. 重新生成 SimpleProject 项目并开始调试。 应显示实验实例

3. 在"**新建Project** 对话框中，单击 **"SimpleProject"** 节点。 控制台 **应用程序** 模板应显示在" **模板"窗格中** 。

4. 展开 **SimpleProject** 节点。 控制台 **子** 节点应显示。 **SimpleProject 应用程序** 模板将继续显示在"**模板"窗格中**。

5. 单击 **"取消** "并停止调试。

    ![简单Project汇总](../extensibility/media/simpproj2_rollup.png "SimpProj2_Rollup")

    ![简单Project控制台节点](../extensibility/media/simpproj2_subfolder.png "SimpProj2_Subfolder")

## <a name="substitute-project-template-parameters"></a>替换项目模板参数
- [创建基本项目系统的第 1](../extensibility/creating-a-basic-project-system-part-1.md) 部分展示了如何覆盖 `ProjectNode.AddFileFromTemplate` 方法以执行基本类型的模板参数替换。 本部分介绍如何使用更复杂的模板Visual Studio参数。

在"新建项目"对话框中Visual Studio模板创建项目时，模板参数 **Project** 字符串来自定义项目。 模板参数是一种以美元符号开头和结尾的特殊令牌，例如，$time$。 以下两个参数对于在基于模板的项目中启用自定义特别有用：

- $GUID[1-10]$ 替换为新的 Guid。 可以指定最多 10 个唯一 GUID，例如 $guid 1$。

- $safeprojectname$ 是用户在"新建Project中提供的名称，经过修改 **以** 删除所有不安全字符和空格。

  有关模板参数的完整列表，请参阅[模板参数](../ide/template-parameters.md)。

### <a name="to-substitute-project-template-parameters"></a>替换项目模板参数

1. 在 *SimpleProjectNode.cs* 文件中，删除 `AddFileFromTemplate` 方法。

2. 在 *\\ Templates\Projects\ConsoleApp\SimpleProject.myproj* 文件中，找到 属性，将属性的值更改为 \<RootNamespace> $safeprojectname$。

    ```
    <RootNamespace>$safeprojectname$</RootNamespace>
    ```

3. 在 *\\ Templates\Projects\SimpleProject\Program.cs* 文件中，将文件的内容替换为以下代码：

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

5. 创建新的 SimpleProject 控制台应用程序。 **("Project"窗格中**，选择"**简单""项目"。** 在 **Visual Studio模板"下，** 选择"**控制台应用程序**.) 

6. 在新建的项目中，打开 *Program.cs*。 它应如下所示， (GUID 值会有所不同。) ：

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
你可以为项目类型创建属性页，以便用户可以查看和更改基于模板的项目的属性。 本部分演示如何创建与配置无关的属性页。 此基本属性页使用属性网格来显示在属性页类中公开的公共属性。

从基类派生属性页 `SettingsPage` 类。 类提供的属性网格 `SettingsPage` 了解大多数基元数据类型，并知道如何显示它们。 此外， `SettingsPage` 类知道如何将属性值保留到项目文件。

通过本部分创建的属性页，可以更改和保存这些项目属性：

- AssemblyName

- OutputType

- RootNamespace。

1. 在 *SimpleProjectPackage.cs* 文件中，将 `ProvideObject` 此属性添加到 `SimpleProjectPackage` 类：

    ```
    [ProvideObject(typeof(GeneralPropertyPage))]
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

    这会向 COM 注册属性页 `GeneralPropertyPage` 类。

2. 在 *SimpleProjectNode.cs* 文件中，将以下两个重写方法添加到 `SimpleProjectNode` 类：

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

    这两种方法都返回属性页 GUID 的数组。 GeneralPropertyPage GUID 是数组中的唯一元素，因此"属性 **页** "对话框将只显示一页。

3. 将名为 *GeneralPropertyPage.cs* 的类文件添加到 SimpleProject 项目。

4. 使用下列代码替换此文件的内容：

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

    类 `GeneralPropertyPage` 公开 AssemblyName、OutputType 和 RootNamespace 这三个公共属性。 由于 AssemblyName 没有 set 方法，因此它显示为只读属性。 OutputType 是一个枚举常量，因此它显示为下拉列表。

    基 `SettingsPage` 类提供 `ProjectMgr` 以保留属性。 `BindProperties`方法使用 `ProjectMgr` 检索持久化属性值并设置相应的属性。 `ApplyChanges`方法使用 `ProjectMgr` 获取属性的值，并保留它们到项目文件。 属性集方法将 `IsDirty` 设置为 true，以指示属性必须持久化。 保存项目或解决方案时发生持久性。

5. 重新生成 SimpleProject 解决方案并开始调试。 应显示实验实例。

6. 在实验实例中，创建新的 SimpleProject 应用程序。

7. Visual Studio调用项目工厂，以使用 Visual Studio 模板创建项目。 新的 *Program.cs* 文件在代码编辑器中打开。

8. 在 中右键单击项目 **解决方案资源管理器，** 然后单击"属性 **"。** 随即显示“属性页”对话框。

    ![简单Project属性页](../extensibility/media/simpproj2_proppage.png "SimpProj2_PropPage")

## <a name="test-the-project-property-page"></a>测试项目属性页
现在，可以测试是否可以修改和更改属性值。

1. 在 **"MyConsoleApplication 属性页** "对话框中，将 **DefaultNamespace** 更改为 **MyApplication**。

2. 选择 **OutputType 属性**，然后选择"**类库"。**

3. 单击“应用”，然后单击“确定”。

4. 重新打开 **"属性页** "对话框，并验证所做的更改是否持久保存。

5. 关闭 Visual Studio 的实验实例。

6. 重新打开实验实例。

7. 重新打开 **"属性页** "对话框，并验证所做的更改是否持久保存。

8. 关闭 Visual Studio 的实验实例。
    ![关闭实验实例](../extensibility/media/simpproj2_proppage2.png "SimpProj2_PropPage2")
