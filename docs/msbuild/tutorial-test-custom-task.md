---
title: 测试自定义任务 | Microsoft Docs
description: 了解如何测试 MSBuild 自定义任务
ms.date: 03/17/2022
ms.topic: tutorial
helpviewer_keywords:
- MSBuild, test custom task
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: d49e6d347cba64bf22fef2b9452dab5f7dbe6b65
ms.sourcegitcommit: 906f8b07e57d2369f64ec42f467f379081f8c5c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2022
ms.locfileid: "141357253"
---
# <a name="tutorial-test-a-custom-task"></a>教程：测试自定义任务

可以使用 Visual Studio 中的单元测试功能以在分发之前测试 MSBuild 自定义任务，从而确保代码的正确性。 有关执行测试和基本测试工具的好处的信息，请参阅[有关单元测试的基础知识](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)。 在本教程中，你将使用其他 MSBuild 自定义任务教程中使用的代码示例。 这些教程中使用的以下项目位于 GitHub 上，其中包括 MSBuild 自定义任务的单元测试和集成测试：

- [自定义任务](tutorial-custom-task-code-generation.md)
- [代码生成](tutorial-rest-api-client-msbuild.md)

## <a name="unit-test"></a>单元测试

MSBuild 自定义任务是继承自 <xref:Microsoft.Build.Utilities.Task> 的类（直接或间接，因为 <xref:Microsoft.Build.Utilities.ToolTask> 继承自 <xref:Microsoft.Build.Utilities.Task>）。 执行与任务关联的操作的方法为 `Execute()`。 此方法采用一些输入值（参数），并且具有可使用断言测试有效性的输出参数。 在这种情况下，一些输入参数是文件的路径，因此此示例在名为 Resources 的文件夹中具有测试输入文件。 此 MSBuild 任务也会生成文件，因此测试断言生成的文件。

需要生成引擎，它是实现 [IBuildEngine](/dotnet/api/microsoft.build.framework.ibuildengine) 的类。 在本示例中，使用 [Moq](https://github.com/Moq/moq4/wiki/Quickstart) 进行模拟，但可以使用其他模拟工具。 该示例收集错误，但你可以收集其他信息，然后对其进行断言。

所有测试都需要 `Engine` 模拟，因此它作为 `TestInitialize` 包括在内（在每个测试之前执行，并且每个测试都有自己的生成引擎）。

有关完整代码，请参阅 GitHub 上的 .NET 示例存储库中的 [AppSettingStronglyTypedTest.cs](https://github.com/dotnet/samples/blob/main/msbuild/custom-task-code-generation/AppSettingStronglyTyped/AppSettingStronglyTyped.Test/AppSettingStronglyTypedTest.cs)。

1. 创建任务并将参数作为测试安排的一部分进行设置：

   ```csharp
       private Mock<IBuildEngine> buildEngine;
       private List<BuildErrorEventArgs> errors;

        [TestInitialize()]
        public void Startup()
        {
            buildEngine = new Mock<IBuildEngine>();
            errors = new List<BuildErrorEventArgs>();
            buildEngine.Setup(x => x.LogErrorEvent(It.IsAny<BuildErrorEventArgs>())).Callback<BuildErrorEventArgs>(e => errors.Add(e));
        }
   ```

1. 创建 <xref:Microsoft.Build.Framework.ITaskItem> 参数模拟（使用 [Moq](https://github.com/Moq/moq4/wiki/Quickstart)），并指向要分析的文件。 然后，使用它的参数创建 `AppSettingStronglyTyped` 自定义任务。 最后，将生成引擎设置为 MSBuild 自定义任务：

   ```csharp
   //Arrange
   var item = new Mock<ITaskItem>();
   item.Setup(x => x.GetMetadata("Identity")).Returns($".\\Resources\\complete-prop.setting");

   var appSettingStronglyTyped = new AppSettingStronglyTyped { SettingClassName = "MyCompletePropSetting", SettingNamespaceName = "MyNamespace", SettingFiles = new[] { item.Object } };

   appSettingStronglyTyped.BuildEngine = buildEngine.Object;
   ```

   然后，执行任务代码以执行实际任务操作：

   ```csharp
    //Act
    var success = appSettingStronglyTyped.Execute();
   ```

1. 最后，断言测试的预期结果：

   ```csharp
   //Assert
   Assert.IsTrue(success); // The execution was success
   Assert.AreEqual(errors.Count, 0); //Not error were found
   Assert.AreEqual($"MyCompletePropSetting.generated.cs", appSettingStronglyTyped.ClassNameFile); // The Task expected output
   Assert.AreEqual(true, File.Exists(appSettingStronglyTyped.ClassNameFile)); // The file was generated
   Assert.IsTrue(File.ReadLines(appSettingStronglyTyped.ClassNameFile).SequenceEqual(File.ReadLines(".\\Resources\\complete-prop-class.txt"))); // Assenting the file content
   ```

1. 其他测试遵循此模式并扩大所有可能性。

> [!NOTE]
> 生成文件时，需要针对每个测试使用不同的文件名以避免冲突。 请记得删除生成的文件作为测试清理。

## <a name="integration-tests"></a>集成测试

单元测试很重要，但还需要在真实的生成上下文中测试自定义 MSBuild 任务。

[System.Diagnostics.Process 类](/dotnet/api/system.diagnostics.process)提供对本地和远程进程的访问权限并使你能够启动和停止本地系统进程。 此示例使用测试 MSBuild 文件对单元测试运行生成。

1. 测试代码需要初始化每个测试的执行上下文。 请注意确保 `dotnet` 命令的路径对于你的环境是准确的。 [此处](https://github.com/dotnet/samples/blob/main/msbuild/custom-task-code-generation/AppSettingStronglyTyped/AppSettingStronglyTyped.Test/AppSettingStronglyTypedIntegrationTest.cs)是完整示例。

   ```csharp
        public const string MSBUILD = "C:\\Program Files\\dotnet\\dotnet.exe";

        private Process buildProcess;
        private List<string> output;

        [TestInitialize()]
        public void Startup()
        {
            output = new List<string>();
            buildProcess = new Process();
            buildProcess.StartInfo.FileName = MSBUILD;
            buildProcess.StartInfo.WindowStyle = ProcessWindowStyle.Hidden;
            buildProcess.StartInfo.CreateNoWindow = true;
            buildProcess.StartInfo.RedirectStandardOutput = true;
        }
   ```

1. 清理时，测试需要完成该过程：

   ```csharp
       [TestCleanup()]
        public void Cleanup()
        {
            buildProcess.Close();
        }
   ```

1. 现在，创建每个测试。 每个测试都需要执行自己的 MSBuild 文件定义。 例如 [testscript-success.msbuild](https://github.com/dotnet/samples/blob/main/msbuild/custom-task-code-generation/AppSettingStronglyTyped/AppSettingStronglyTyped.Test/Resources/testscript-success.msbuild)。 若要了解该文件，请参阅[教程：创建自定义任务](tutorial-custom-task-code-generation.md)。

   ```xml
   <Project Sdk="Microsoft.NET.Sdk">
       <UsingTask TaskName="AppSettingStronglyTyped.AppSettingStronglyTyped" AssemblyFile="..\AppSettingStronglyTyped.dll" />
       <PropertyGroup>
           <TargetFramework>netstandard2.1</TargetFramework>
       </PropertyGroup>

       <PropertyGroup>
           <SettingClass>MySettingSuccess</SettingClass>
           <SettingNamespace>example</SettingNamespace>
       </PropertyGroup>

       <ItemGroup>
           <SettingFiles Include="complete-prop.setting" />
       </ItemGroup>

       <Target Name="generateSettingClass">
           <AppSettingStronglyTyped SettingClassName="$(SettingClass)" SettingNamespaceName="$(SettingNamespace)" SettingFiles="@(SettingFiles)">
               <Output TaskParameter="ClassNameFile" PropertyName="SettingClassFileName" />
           </AppSettingStronglyTyped>
       </Target>
   </Project>
   ```

1. 测试参数提供生成此 MSBuild 文件的说明：

   ```csharp
    //Arrage
    buildProcess.StartInfo.Arguments = "build .\\Resources\\testscript-success.msbuild /t:generateSettingClass";
   ```

1. 执行并获取输出：

   ```csharp
   //Act
   ExecuteCommandAndCollectResults();
   ```

   其中 `ExecuteCommandAndCollectResults()` 定义为：

   ```csharp
   private void ExecuteCommandAndCollectResults()
   {
        buildProcess.Start();
        while (!buildProcess.StandardOutput.EndOfStream)
        {
            output.Add(buildProcess.StandardOutput.ReadLine() ?? string.Empty);
        }
        buildProcess.WaitForExit();
   }
   ```

1. 最后，评估预期结果：

   ```csharp
   //Assert
   Assert.AreEqual(0, buildProcess.ExitCode); //Finished success
   Assert.IsTrue(File.Exists(".\\Resources\\MySettingSuccess.generated.cs")); // the expected resource was generated
   Assert.IsTrue(File.ReadLines(".\\Resources\\MySettingSuccess.generated.cs").SequenceEqual(File.ReadLines(".\\Resources\\testscript-success-class.txt"))); // asserting the file content
   ```

## <a name="conclusion"></a>结论

单元测试很有用，因为你可以测试和调试代码以确保每个特定代码段的正确性，但集成测试对于确保任务在真实的生成上下文中执行非常重要。 在本教程中，你了解了如何测试 MSBuild 自定义任务。

## <a name="next-steps"></a>后续步骤

创建用于执行 REST API 代码生成的更为复杂的自定义任务。

> [!div class="nextstepaction"]
> [使用 MSBuild 生成 REST API 客户端](tutorial-rest-api-client-msbuild.md)
