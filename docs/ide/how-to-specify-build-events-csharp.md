---
title: 如何：指定生成事件 (C#)
description: 了解如何使用生成事件指定生成开始之前或生成完成之后运行的命令。
ms.custom: SEO-VS-2020
ms.date: 03/04/2022
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
  - pre-build events
  - 'events [Visual Studio], builds'
  - post-build events
  - 'build events [Visual Studio]'
  - 'builds [Visual Studio], events'
ms.assetid: b4ce1ad9-5215-4b6f-b6a2-798b249aa335
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
  - dotnet
---
# <a name="how-to-specify-build-events-c"></a>如何：指定生成事件 (C#)

使用生成事件，可以指定生成开始之前或生成完成之后运行的命令。

项目生成时，生成前事件将被添加到名为 PreBuildEvent.bat 的文件，而生成后事件将被添加到名为 PostBuildEvent.bat 的文件。 若要确保错误检查，请向生成步骤中添加自己的错误检查命令。

## <a name="specify-a-build-event"></a>指定生成事件

:::moniker range="<=vs-2019"

1. 在“解决方案资源管理器”中，选择要为其指定生成事件的项目  。

2. 在 **“项目”** 菜单上，单击 **“属性”** 。

3. 选择“生成事件”选项卡。

4. 在“预先生成事件命令行”框中指定生成事件的语法。

   > [!NOTE]
   > 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。

5. 在“后期生成事件命令行”框中指定生成事件的语法。

   > [!NOTE]
   > 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。

6. 在“运行后期生成事件”框中，指定运行后期生成事件的条件。

   > [!NOTE]
   > 若要添加长语法，或从[预先生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)中选择任何生成宏，请单击省略号按钮 (…) 以显示编辑框。

:::moniker-end
:::moniker range=">=vs-2022"

1. 在“解决方案资源管理器”中，选择要为其指定生成事件的项目  。

2. 在 " **Project** " 菜单上，单击 "**属性**" (或从 **解决方案资源管理器** 中，按 **Alt** + **enter**) 。

3. 选择 " **生成 > 事件**"。

   ![显示生成事件设置的屏幕截图。](media/vs-2022/build-events.png)

4. 在 " **预生成事件** " 部分中，指定生成事件的语法。

   > [!NOTE]
   > 如果项目是最新的且没有触发任何生成，则不会运行预生成事件。

5. 在 " **生成后事件** " 部分中，指定生成事件的语法。

   > [!NOTE]
   > 在运行 .bat 文件的所有生成后命令之前添加 `call` 语句。 例如，`call C:\MyFile.bat` 或 `call C:\MyFile.bat call C:\MyFile2.bat`。

6. 在 " **要在何时运行生成后事件** " 部分中，指定在什么条件下运行生成后事件。

:::moniker-end

生成事件语法可以包含命令提示符处或 .bat 文件中有效的任何命令。 批处理文件名的前面应带有 `call`，以确保执行后面的所有命令。

> [!NOTE]
> 如果预生成事件或生成后事件未成功完成，可通过使用除零 (0) 之外的代码退出事件操作来终止生成，这表示操作成功。

## <a name="macros"></a>宏

通常可用的 "宏" (实际上 MSBuild 属性) 列在[MSBuild 通用属性](../msbuild/common-msbuild-project-properties.md)中。 对于 .net SDK 项目 ( .net Core 或 .net 5 及更高版本) ，其他属性在[Microsoft 的 MSBuild 属性](/dotnet/core/project-sdk/msbuild-props)中列出。

在您的脚本中生成事件时，您可能希望引用某些项目级别变量的值，例如项目的名称或输出文件夹的位置。 在 Visual Studio 的以前版本中，这些称为 "*宏*"。 与最新版本的 Visual Studio 中的宏等效的 MSBuild 属性。 MSBuild 是 Visual Studio 在执行生成时用于处理项目文件的生成引擎。 IDE 中的生成事件会导致项目文件中出现 MSBuild[目标](../msbuild/msbuild-targets.md)。 你可以使用项目文件中的目标中可用的任何 MSBuild 属性 (例如 `$(OutDir)` 或 `$(Configuration)`) 。 这些事件中可用的 MSBuild 属性取决于在项目文件 `.props` `.targets` （如元素）中隐式或显式导入的文件（如文件）和属性（如元素中 `PropertyGroup` ）。 请小心地使用每个属性的拼写。 如果属性拼写错误，则不会报告任何错误;相反，未定义的属性的计算结果为空字符串。

例如，假设您指定了一个预先生成事件，如下所示：

![显示预先生成事件示例的屏幕截图。](./media/vs-2022/pre-build-event-example.png)

该预生成事件会生成以下条目，该项在项目文件中称为 `Target` ：

```xml
  <Target Name="PreBuild" BeforeTargets="PreBuildEvent">
    <Exec Command="echo Configuration: $(Configuration)&#xD;&#xA;echo DevEnvDir: $(DevEnvDir)&#xD;&#xA;echo OutDir: $(OutDir)&#xD;&#xA;echo ProjectDir: $(ProjectDir)&#xD;&#xA;echo VisualStudioVersion: $(VisualStudioVersion)&#xD;&#xA;echo AssemblySearchPaths: $(AssemblySearchPaths)&#xD;&#xA;echo AssemblyName: $(AssemblyName)&#xD;&#xA;echo BaseIntermediateOutputPath: $(BaseIntermediateOutputPath)&#xD;&#xA;echo CscToolPath: $(CscToolPath)" />
  </Target>
```

生成事件显示为一个目标，其中包含具有指定为的 `Command` 输入的[Exec 任务](../msbuild/exec-task.md)。 在 XML 中对换行符进行编码。

在此示例中生成项目时，预先生成事件将打印某些属性的值。 在此示例中， `$(CscToolPath)` 不会生成任何输出，因为它未定义。 这是一个可选属性，可在项目文件中定义，以提供 c # 编译器的自定义实例的路径 (例如，如果您要测试 *csc.exe* 的不同版本，或实验编译器) 。

生成事件的输出将写入生成输出，这些输出可在 **输出** 窗口中找到。 在 " **显示输出来源** " 下拉列表中，选择 " **生成**"。

```output
Build started...
1>------ Build started: Project: ConsoleApp4, Configuration: Debug Any CPU ------
1>You are using a preview version of .NET. See: https://aka.ms/dotnet-core-preview
1>Configuration: Debug
1>DevEnvDir: C:\Program Files\Microsoft Visual Studio\2022\Preview\Common7\IDE\
1>OutDir: bin\Debug\net6.0\
1>ProjectDir: C:\source\repos\ConsoleApp4\ConsoleApp4\
1>VisualStudioVersion: 17.0
1>ALToolsPath:
1>AssemblySearchPaths: {CandidateAssemblyFiles};{HintPathFromItem};{TargetFrameworkDirectory};{RawFileName}
1>AssemblyName: ConsoleApp4
1>BaseIntermediateOutputPath: obj\
1>CscToolsPath:
1>Skipping analyzers to speed up the build. You can execute 'Build' or 'Rebuild' command to run analyzers.
1>ConsoleApp4 -> C:\Users\ghogen\source\repos\ConsoleApp4\ConsoleApp4\bin\Debug\net6.0\ConsoleApp4.dll
```

## <a name="example"></a>示例

下面的过程说明如何使用从生成后事件（项目目录中的 .exe.manifest 文件）中调用的 .exe 命令设置应用程序清单中的操作系统最低版本。 最低的操作系统版本是由四个部分组成的数字组合，例如 4.10.0.0。 要设置最低操作系统版本，命令将更改 `<dependentOS>` 清单的部分：

```xml
<dependentOS>
   <osVersionInfo>
      <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   </osVersionInfo>
</dependentOS>
```

### <a name="create-an-exe-command-to-change-the-application-manifest"></a>创建 .exe 命令以更改应用程序清单

1. 为命令创建新的“控制台应用”项目。 将项目命名为 ChangeOSVersionCS。

2. 在 Program.cs 中，将以下行添加到文件顶部的其他 `using` 指令：

   ```csharp
   using System.Xml;
   ```

3. 在 `ChangeOSVersionCS` 命名空间中，将 `Program` 类实现替换为以下代码：

   ```csharp
   class Program
   {
      /// <summary>
      /// This function sets the minimum operating system version for a ClickOnce application.
      /// </summary>
      /// <param name="args">
      /// Command Line Arguments:
      /// 0 - Path to application manifest (.exe.manifest)
      /// 1 - Version of OS
      ///</param>
      static void Main(string[] args)
      {
         string applicationManifestPath = args[0];
         Console.WriteLine("Application Manifest Path: " + applicationManifestPath);

         // Get version name.
         Version osVersion = null;
         if (args.Length >=2 ){
            osVersion = new Version(args[1]);
         }else{
            throw new ArgumentException("OS Version not specified.");
         }
         Console.WriteLine("Desired OS Version: " + osVersion.ToString());

         XmlDocument document;
         XmlNamespaceManager namespaceManager;
         namespaceManager = new XmlNamespaceManager(new NameTable());
         namespaceManager.AddNamespace("asmv1", "urn:schemas-microsoft-com:asm.v1");
         namespaceManager.AddNamespace("asmv2", "urn:schemas-microsoft-com:asm.v2");

         document = new XmlDocument();
         document.Load(applicationManifestPath);

         string baseXPath;
         baseXPath = "/asmv1:assembly/asmv2:dependency/asmv2:dependentOS/asmv2:osVersionInfo/asmv2:os";

         // Change minimum required operating system version.
         XmlNode node;
         node = document.SelectSingleNode(baseXPath, namespaceManager);
         node.Attributes["majorVersion"].Value = osVersion.Major.ToString();
         node.Attributes["minorVersion"].Value = osVersion.Minor.ToString();
         node.Attributes["buildNumber"].Value = osVersion.Build.ToString();
         node.Attributes["servicePackMajor"].Value = osVersion.Revision.ToString();

         document.Save(applicationManifestPath);
      }
   }
   ```

   此命令采用两个参数：应用程序清单的路径（即生成进程在其中创建清单的文件夹，通常为 Projectname.publish），以及新的操作系统版本。

4. 生成项目。

5. 将 .exe 文件复制到类似于 C:\TEMP\ChangeOSVersionVB.exe 的目录 。

然后，在后期生成事件中调用此命令以修改应用程序清单。

### <a name="invoke-a-post-build-event-to-modify-the-application-manifest"></a>调用生成后事件以修改应用程序清单

1. 创建新的“Windows 窗体应用”项目，并将其命名为 CSWinApp。

2. 在“解决方案资源管理器”中选择一个项目，然后在“项目”菜单上选择“属性”。

3. 在项目设计器中，转到“发布”页，并将“发布位置”设置为 C:\TEMP。

4. 单击“立即发布”以发布项目。

   系统随即生成清单文件并将其保存到 C:\TEMP\CSWinApp_1_0_0_0\CSWinApp.exe.manifest。 若要查看该清单，请右键单击该文件，单击“打开方式”，选择“从列表中选择程序”，然后单击“记事本”。

   在文件中搜索 `<osVersionInfo>` 元素。 例如，版本可能为：

   ```xml
   <os majorVersion="4" minorVersion="10" buildNumber="0" servicePackMajor="0" />
   ```

5. 返回 **Project 设计器** 中，单击 "**生成事件**" 选项卡。

6. 在 " **生成后事件** " 部分中，输入以下命令：

   `C:\TEMP\ChangeOSVersionCS.exe "$(TargetPath).manifest" 5.1.2600.0`

   生成项目时，此命令会将应用程序清单中的最低操作系统版本更改为 5.1.2600.0。

   由于 `$(TargetPath)` 宏表示所创建的可执行文件的完整路径，因此 `$(TargetPath).manifest` 将指定在 bin 目录中创建的应用程序清单。 发布操作会将此清单复制到之前设置的发布位置。

7. 再次发布该项目。

   清单版本现在应显示为：

   ```xml
   <os majorVersion="5" minorVersion="1" buildNumber="2600" servicePackMajor="0" />
   ```

> [!NOTE]
> 某些方案可能需要更多的智能生成操作，而不是生成事件。 例如，对于许多常见的代码生成方案，你需要处理清理和重新生成操作，并且你可能希望为代码生成步骤启用增量生成，以便仅当输出对于输入过期时才运行该步骤。 对于这种情况，请考虑创建一个 [自定义目标](../msbuild/target-build-order.md) ，以指定 `AfterTargets` `BeforeTargets` 要在生成过程中的特定时间点运行，并在高级方案中进一步控制，请考虑创建 [自定义任务](../msbuild/task-writing.md)。

## <a name="see-also"></a>另请参阅

- [项目设计器的“生成事件”页 (C#)](../ide/reference/build-events-page-project-designer-csharp.md)
- [预生成事件/生成后事件命令行对话框](../ide/reference/pre-build-event-post-build-event-command-line-dialog-box.md)
- [如何：指定生成事件 (Visual Basic)](../ide/how-to-specify-build-events-visual-basic.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
