---
title: 创建基本 Project 系统，第1部分 |Microsoft Docs
description: 了解如何创建名为 myproj.csproj 的项目类型。 在 Visual Studio 中，项目是用于组织源代码文件和其他资产的容器。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: c24fc5a1e685c80cbc1d122538fbcbae520995614591085effed104e6e094215
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403414"
---
# <a name="create-a-basic-project-system-part-1"></a>创建基本项目系统，第1部分
在 Visual Studio 中，项目是开发人员用来组织源代码文件和其他资产的容器。 项目在 **解决方案资源管理器** 中显示为解决方案的子项目。 项目使你可以组织、构建、调试和部署源代码，并创建对 Web 服务、数据库和其他资源的引用。

 项目是在项目文件中定义的，例如 Visual c # 项目的 *.csproj* 文件。 你可以创建自己的项目类型，它具有自己的项目文件扩展名。 有关项目类型的详细信息，请参阅[Project 类型](../extensibility/internals/project-types.md)。

> [!NOTE]
> 如果需要使用自定义项目类型扩展 Visual Studio，我们强烈建议使用[Visual Studio 项目系统](https://github.com/Microsoft/VSProjectSystem) (.vsps) ，该系统与从头开始构建项目系统相比，它具有许多优势：
>
> - 更轻松的载入。  即使是基本的项目系统也需要数十个代码行。  利用 .VSPS，你可以在准备好根据你的需求进行自定义之前，只需单击几下即可。
> - 更易于维护。  利用 .VSPS，只需维护自己的方案即可。  我们处理所有项目系统基础结构的保养。
>
>   如果需要将低于 Visual Studio 2013 Visual Studio 版本作为目标，将无法在 Visual Studio 扩展中利用 .vsps。  如果是这种情况，则可以使用此演练。

 本演练演示如何创建项目文件扩展名为 *myproj.csproj* 的项目类型。 本演练将借用现有 Visual c # 项目系统。

> [!NOTE]
> 有关扩展项目的更多示例，请参阅 [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples)。

 本演练介绍了如何完成以下任务：

- 创建基本项目类型。

- 创建基本项目模板。

- 将项目模板注册 Visual Studio。

- 通过打开 "**新建 Project** " 对话框，然后使用模板来创建项目实例。

- 为项目系统创建项目工厂。

- 为项目系统创建项目节点。

- 为项目系统添加自定义图标。

- 实现基本模板参数替换。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不会从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

 还必须下载 [项目的托管包框架](https://github.com/tunnelvisionlabs/MPFProj10)的源代码。 将文件提取到要创建的解决方案可访问的位置。

## <a name="create-a-basic-project-type"></a>创建基本项目类型
 创建一个名为 **SimpleProject** 的 c # VSIX 项目。  (**文件**  >  **新**  >  **Project** ，然后 **Visual c #**  >  **扩展性**  >  **VSIX Project**) 。 添加 Visual Studio 包项目项模板 (在 **解决方案资源管理器** 上，右键单击项目节点并选择 "**添加**  >  **新项**"，然后中转到 "**扩展性**  >  **Visual Studio 包**) "。 将该文件命名为 *SimpleProjectPackage*。

## <a name="creating-a-basic-project-template"></a>创建基本项目模板
 现在，可以修改此基本 VSPackage 以实现 *myproj.csproj* 项目类型。 若要创建基于 *. myproj.csproj* 项目类型的项目，Visual Studio 必须知道要添加到新项目中的文件、资源和引用。 若要提供此信息，请将项目文件放在项目模板文件夹中。 当用户使用 *myproj.csproj* 项目创建项目时，文件将复制到新项目。

### <a name="to-create-a-basic-project-template"></a>创建基本项目模板

1. 向项目添加三个文件夹，一个文件夹位于另一个文件夹中： *Templates\Projects\SimpleProject*。  (在 **解决方案资源管理器** 中，右键单击 **SimpleProject** 项目节点，指向 " **添加**"，然后单击 " **新建文件夹**"。 命名文件夹 *模板*。 在 " *模板* " 文件夹中，添加一个名为 " *项目*" 的文件夹。 在 " *项目* " 文件夹中，添加名为 *SimpleProject* 的文件夹。 ) 

2. 在 *Templates\Projects\SimpleProject* 文件夹中，添加要用作名为 *SimpleProject* 的图标的位图图像文件。 单击 " **添加**" 时，图标编辑器将打开。

3. 使图标与众不同。 此图标将显示在本演练后面的 "**新建 Project** " 对话框中。

    ![“简单项目”图标](../extensibility/media/simpleprojicon.png "SimpleProjIcon")

4. 保存图标，并关闭图标编辑器。

5. 在 *Templates\Projects\SimpleProject* 文件夹中，添加一个名为 *Program .cs* 的 **类** 项。

6. 将现有代码替换为以下行。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Text;

   namespace $nameSpace$
   {
       public class $className$
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

   > [!IMPORTANT]
   > 这不是 *程序 .cs* 代码的最终形式;稍后的步骤中将会处理替换参数。 你可能会看到编译错误，但是只要该文件的 **BuildAction** 是 **内容**，你就可以像平常一样生成并运行该项目。

7. 保存文件。

8. 将 *AssemblyInfo* 文件从 *Properties* 文件夹复制到 *Projects\SimpleProject* 文件夹。

9. 在 *Projects\SimpleProject* 文件夹中，添加名为 *SimpleProject. myproj.csproj* 的 XML 文件。

   > [!NOTE]
   > 此类型的所有项目的文件扩展名为 *myproj.csproj*。 如果要对其进行更改，必须在本演练所述的任何位置对其进行更改。

10. 将现有内容替换为以下行。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid></ProjectGuid>
        <OutputType>Exe</OutputType>
        <RootNamespace>MyRootNamespace</RootNamespace>
        <AssemblyName>MyAssemblyName</AssemblyName>
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        <DebugSymbols>true</DebugSymbols>
        <OutputPath>bin\Debug\</OutputPath>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
        <DebugSymbols>false</DebugSymbols>
        <OutputPath>bin\Release\</OutputPath>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="mscorlib" />
        <Reference Include="System" />
        <Reference Include="System.Data" />
        <Reference Include="System.Xml" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="AssemblyInfo.cs">
          <SubType>Code</SubType>
        </Compile>
        <Compile Include="Program.cs">
          <SubType>Code</SubType>
        </Compile>
      </ItemGroup>
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

11. 保存文件。

12. 在 "**属性**" 窗口中，将 " *AssemblyInfo*"、"SimpleProject *"、*" *SimpleProject*" 和 " *myproj.csproj* " 的 "**生成" 操作** 设置为 "**内容**"，并将其 **"包含项**" 设置为 " **True**"。

    此项目模板描述了一个基本的 Visual c # 项目，该项目同时具有 "调试" 配置和 "发布" 配置。 该项目包括两个源文件： *AssemblyInfo* *和 .cs 以及若干* 程序集引用。 当从模板创建项目时，ProjectGuid 值会自动替换为新的 GUID。

    在 **解决方案资源管理器** 中，展开的 " **模板** " 文件夹应如下所示：

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>创建基本项目工厂
 必须告知 Visual Studio 项目模板文件夹的位置。 为此，请将特性添加到实现项目工厂的 VSPackage 类，以便在生成 VSPackage 时将模板位置写入系统注册表。 首先，创建一个由项目工厂 GUID 标识的基本项目工厂。 使用 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> 属性将项目工厂连接到 `SimpleProjectPackage` 类。

### <a name="to-create-a-basic-project-factory"></a>创建基本项目工厂

1. 为项目工厂创建 Guid (在 " **工具** " 菜单上，单击 " **创建 GUID** ") ，或使用以下示例中的一个。 将 Guid 添加到 `SimpleProjectPackage` 已定义的节附近的类中 `PackageGuidString` 。 Guid 必须采用 GUID 格式和字符串格式。 生成的代码应类似于以下示例。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. 将一个类添加到名为 *SimpleProjectFactory* 的顶级 *SimpleProject* 文件夹中。

3. 添加以下 using 指令：

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. 将 GUID 特性添加到 `SimpleProjectFactory` 类。 该属性的值为新的项目工厂 GUID。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   现在可以注册项目模板。

### <a name="to-register-the-project-template"></a>注册项目模板

1. 在 *SimpleProjectPackage* 中，将属性添加 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> 到 `SimpleProjectPackage` 类，如下所示。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. 重新生成解决方案并验证它是否生成但未发生错误。

    重新生成将注册项目模板。

   参数 `defaultProjectExtension` 和 `possibleProjectExtensions` 设置为项目文件扩展名 (*myproj.csproj*) 。 `projectTemplatesDirectory`参数设置为 *Templates* 文件夹的相对路径。 在生成过程中，此路径将转换为完整生成并添加到注册表中，以注册项目系统。

## <a name="test-the-template-registration"></a>测试模板注册
 模板注册会告诉 Visual Studio 项目模板文件夹的位置，以便 Visual Studio 可以在 "**新建 Project** " 对话框中显示模板名称和图标。

### <a name="to-test-the-template-registration"></a>测试模板注册

1. 按 **F5** 开始调试 Visual Studio。

2. 在实验实例中，创建新创建的项目类型的新项目。 在 **"新建Project"** 对话框中，应看到"已安装模板"下的 **"SimpleProject"。** 

   现在，你有一个已注册的项目工厂。 但是，它尚无法创建项目。 项目包和项目工厂协同工作来创建和初始化项目。

## <a name="add-the-managed-package-framework-code"></a>添加托管包框架代码
 实现项目包与项目工厂之间的连接。

- 导入托管包框架的源代码文件。

    1. 在 解决方案资源管理器 中卸载 SimpleProject 项目 **(，选择** 项目节点，在上下文菜单上单击"卸载 **Project**.) "，在 XML 编辑器中打开项目文件。

    2. 将以下块添加到项目文件， (块 \<Import> 正上方) 。 设置为 `ProjectBasePath` 刚刚下载的托管包框架代码中 *ProjectBase.files* 文件的位置。 可能需要将反杠添加到 pathname。 如果没有，则项目可能无法找到托管包框架源代码。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > 不要忘记路径末尾的反杠。

    3. 重新加载项目。

    4. 添加对下列程序集的引用：

        - `Microsoft.VisualStudio.Designer.Interfaces` (*\<VSSDK install> \VisualStudioIntegration\Common\Assemblies\v2.0*) 

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>初始化项目工厂

1. 在 *SimpleProjectPackage.cs* 文件中，添加以下 `using` 指令。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. 从 `SimpleProjectPackage` 派生类 `Microsoft.VisualStudio.Package.ProjectPackage` 。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. 注册项目工厂。 将以下行添加到 `SimpleProjectPackage.Initialize` 方法，就在 之后 `base.Initialize` 。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 实现抽象属性 `ProductUserContext` ：

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. 在 *SimpleProjectFactory.cs* 中，将以下 `using` 指令添加到现有 `using` 指令之后。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. 从 `SimpleProjectFactory` 派生类 `ProjectFactory` 。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 将以下虚拟方法添加到 `SimpleProjectFactory` 类。 稍后部分将实现此方法。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 将以下字段和构造函数添加到 `SimpleProjectFactory` 类。 此 `SimpleProjectPackage` 引用缓存在私有字段中，以便可用于设置服务提供商站点。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. 重新生成解决方案并验证其生成是否未出错。

## <a name="test-the-project-factory-implementation"></a>测试项目工厂实现
 测试是否调用项目工厂实现构造函数。

### <a name="to-test-the-project-factory-implementation"></a>测试项目工厂实现

1. 在 *SimpleProjectFactory.cs* 文件中，在构造函数中的以下行上设置 `SimpleProjectFactory` 断点。

    ```csharp
    this.package = package;
    ```

2. 按 **F5** 启动 Visual Studio。

3. 在实验实例中，开始创建新项目。 在"**新建Project"** 对话框中，选择 **"SimpleProject"** 项目类型，然后单击"确定 **"。** 执行在断点处停止。

4. 清除断点并停止调试。 由于我们尚未创建项目节点，因此项目创建代码仍会引发异常。

## <a name="extend-the-projectnode-class"></a>扩展 ProjectNode 类
 现在，你可以实现 `SimpleProjectNode` 类，该类派生自 `ProjectNode` 类。 基 `ProjectNode` 类处理以下项目创建任务：

- 将项目模板文件 *SimpleProject.myproj* 复制到新项目文件夹。 该副本根据在"新建帐户"对话框中输入的名称 **Project** 重命名。 `ProjectGuid`属性值将替换为新的 GUID。

- 遍历MSBuild模板文件 *SimpleProject.myproj* 的一些元素，并查找 `Compile` 元素。 对于每个 `Compile` 目标文件，将该文件复制到新项目文件夹。

  派生类 `SimpleProjectNode` 处理以下任务：

- 启用要创建或选择 **解决方案资源管理器和文件** 节点的图标。

- 允许指定其他项目模板参数替换。

### <a name="to-extend-the-projectnode-class"></a>扩展 ProjectNode 类

1. 添加名为的 `SimpleProjectNode.cs` 的类。

2. 用下面的代码替换现有代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Project;

   namespace SimpleProject
   {
       public class SimpleProjectNode : ProjectNode
       {
           private SimpleProjectPackage package;

           public SimpleProjectNode(SimpleProjectPackage package)
           {
               this.package = package;
           }
           public override Guid ProjectGuid
           {
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
           }
           public override string ProjectType
           {
               get { return "SimpleProjectType"; }
           }

           public override void AddFileFromTemplate(
               string source, string target)
           {
               this.FileTemplateProcessor.UntokenFile(source, target);
               this.FileTemplateProcessor.Reset();
           }
       }
   }
   ```

   此类 `SimpleProjectNode` 实现具有以下重写方法：

- `ProjectGuid`，它返回项目工厂 GUID。

- `ProjectType`，返回项目类型的本地化名称。

- `AddFileFromTemplate`，将所选文件从模板文件夹复制到目标项目。 此方法在稍后部分中进一步实现。

  构造函数 `SimpleProjectNode` 与构造函数 `SimpleProjectFactory` 一样，将引用 `SimpleProjectPackage` 缓存在私有字段中供以后使用。

  若要将 类连接到 类，必须在 方法中实例化新的 ，将其缓存在私有 `SimpleProjectFactory` `SimpleProjectNode` `SimpleProjectNode` `SimpleProjectFactory.CreateProject` 字段中供以后使用。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>连接项目工厂类和节点类

1. 在 *SimpleProjectFactory.cs* 文件中，添加以下 `using` 指令：

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. 使用 `SimpleProjectFactory.CreateProject` 下面的代码替换 方法。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. 重新生成解决方案并验证其生成是否未出错。

## <a name="test-the-projectnode-class"></a>测试 ProjectNode 类
 测试项目工厂，看它是否创建项目层次结构。

### <a name="to-test-the-projectnode-class"></a>测试 ProjectNode 类

1. 按 **F5** 启动调试。 在实验实例中，创建新的 SimpleProject。

2. Visual Studio调用项目工厂以创建项目。

3. 关闭 Visual Studio 的实验实例。

## <a name="add-a-custom-project-node-icon"></a>添加自定义项目节点图标
 上一部分中的项目节点图标是默认图标。 可更改为自定义图标。

### <a name="to-add-a-custom-project-node-icon"></a>添加自定义项目节点图标

1. 在 Resources **文件夹中**，添加名为 的位图 *SimpleProjectNode.bmp。*

2. 在" **属性** "窗口中，将位图减少 16 x 16 像素。 使位图独一无二。

    ![简单项目命令](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")

3. 在"**属性"** 窗口中，将位 **图** 的"生成"操作更改为 **"嵌入资源"。**

4. 在 *SimpleProjectNode.cs* 中，添加以下 `using` 指令：

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 将以下静态字段和构造函数添加到 `SimpleProjectNode` 类。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. 将以下属性添加到 类的 `SimpleProjectNode` 开头。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. 将 实例构造函数替换为以下代码。

   ```csharp
   public SimpleProjectNode(SimpleProjectPackage package)
   {
       this.package = package;

       imageIndex = this.ImageHandler.ImageList.Images.Count;

       foreach (Image img in imageList.Images)
       {
           this.ImageHandler.AddImage(img);
       }
   }
   ```

   在静态构造期间， 从程序集清单资源中检索项目节点位图，并缓存在私有 `SimpleProjectNode` 字段中供以后使用。 请注意图像路径 <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> 的语法。 若要查看嵌入程序集中的清单资源的名称，请使用 <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> 方法。 将此方法应用于程序集 `SimpleProject` 时，结果应如下所示：

- *SimpleProject.Resources.resources*

- *VisualStudio。Project.resources*

- *SimpleProject.VSPackage.resources*

- *Resources.imagelis.bmp*

- *Microsoft.VisualStudio。Project。DontShowAgainDialog.resources*

- *Microsoft.VisualStudio。Project。SecurityWarningDialog.resources*

- *SimpleProject.Resources.SimpleProjectNode.bmp*

  在实例构造期间，基类加载Resources.imagelis.bmp，其中嵌入了中常用的 `ProjectNode` 16 ** x 16 位Resources\imagelis.bmp。 ** 此位图列表以 格式 `SimpleProjectNode` 提供给 `ImageHandler.ImageList` 。 `SimpleProjectNode` 将项目节点位图追加到列表。 将缓存 "图像" 列表中项目节点位图的偏移量，以便以后将其用作公共属性的值 `ImageIndex` 。 Visual Studio 使用此属性来确定显示为项目节点图标的位图。

## <a name="test-the-custom-project-node-icon"></a>测试自定义项目节点图标
 测试项目工厂，以查看它是否创建了包含自定义项目节点图标的项目层次结构。

### <a name="to-test-the-custom-project-node-icon"></a>测试 "自定义项目节点" 图标

1. 开始调试，并在实验实例中创建新的 SimpleProject。

2. 请注意，在新创建的项目中，将 *SimpleProjectNode.bmp* 用作项目节点图标。

     ![简单项目“新建项目节点”](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")

3. 在代码编辑器中打开“Program.cs”。 应会看到类似于以下代码的源代码。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace $nameSpace$
    {
        public class $className$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

     请注意，$nameSpace $ 和 $className $ 的模板参数没有新值。 在下一部分中，你将学习如何实现模板参数替换。

## <a name="substitute-template-parameters"></a>替换模板参数
 在前面的部分中，已使用属性将项目模板注册 Visual Studio `ProvideProjectFactory` 。 通过以这种方式注册模板文件夹的路径，可以通过重写和扩展类来启用基本模板参数替换 `ProjectNode.AddFileFromTemplate` 。 有关详细信息，请参阅 [新项目生成：在幕后，第二部分](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)。

 现在，将替换代码添加到 `AddFileFromTemplate` 类。

### <a name="to-substitute-template-parameters"></a>替换模板参数

1. 在 *SimpleProjectNode* 文件中，添加以下 `using` 指令。

   ```csharp
   using System.IO;
   ```

2. `AddFileFromTemplate`使用以下代码替换方法。

   ```csharp
   public override void AddFileFromTemplate(
       string source, string target)
   {
       string nameSpace =
           this.FileTemplateProcessor.GetFileNamespace(target, this);
       string className = Path.GetFileNameWithoutExtension(target);

       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);
       this.FileTemplateProcessor.AddReplace("$className$", className);

       this.FileTemplateProcessor.UntokenFile(source, target);
       this.FileTemplateProcessor.Reset();
   }
   ```

3. 在方法中设置断点，就在 `className` 赋值语句之后。

   赋值语句确定命名空间和新类名的合理值。 这两个 `ProjectNode.FileTemplateProcessor.AddReplace` 方法调用使用这些新值替换相应的模板参数值。

## <a name="test-the-template-parameter-substitution"></a>测试模板参数替换
 现在可以测试模板参数替换。

### <a name="to-test-the-template-parameter-substitution"></a>测试模板参数替换

1. 开始调试，并在实验实例中创建新的 SimpleProject。

2. 执行在方法中的断点处停止 `AddFileFromTemplate` 。

3. 检查和参数的值 `nameSpace` `className` 。

   - `nameSpace` 提供 \<RootNamespace> *\Templates\Projects\SimpleProject\SimpleProject.myproj* 项目模板文件中元素的值。 在本例中，该值为 `MyRootNamespace`。

   - `className` 为提供类源文件名的值，没有文件扩展名。 在这种情况下，要复制到目标文件夹的第一个文件为 *AssemblyInfo*;因此，className 的值为 `AssemblyInfo` 。

4. 删除断点，然后按 **F5** 继续执行。

    Visual Studio 应完成创建项目。

5. 在代码编辑器中打开“Program.cs”。 应会看到类似于以下代码的源代码。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;

   namespace MyRootNamespace
   {
       public class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

    请注意，命名空间现在为 `MyRootNamespace` ，类名称现在为 `Program` 。

6. 开始调试项目。 新项目应编译、运行和显示 "Hello VSX!!!" 显示文本字符串“Hello World!”。

    ![简单项目命令](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")

   祝贺你！ 您已经实现了一个基本的托管项目系统。
