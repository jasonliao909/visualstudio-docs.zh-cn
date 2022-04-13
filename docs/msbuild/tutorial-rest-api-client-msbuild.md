---
title: 在生成中处理代码生成
description: 了解如何通过使用 Exec 任务运行工具，或通过创建自定义任务来编辑 MSBuild 项目文件以处理代码生成（例如 REST API 客户端生成）。
ms.date: 03/07/2022
ms.topic: tutorial
helpviewer_keywords:
- MSBuild, tutorial
- MSBuild, code generation
author: ghogen
ms.author: ghogen
manager: jmartens
ms.technology: msbuild
ms.workload:
- multiple
ms.openlocfilehash: 127c3ae3c9cea5d7aa17b67b4af29e593df2f738
ms.sourcegitcommit: 906f8b07e57d2369f64ec42f467f379081f8c5c8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2022
ms.locfileid: "141357255"
---
# <a name="tutorial-generate-a-rest-api-client"></a>教程：生成 REST API 客户端

使用 REST API 的应用程序是一个极为常见的方案。 通常，需要生成应用程序可用来调用 REST API 的客户端代码。 在本教程中，你将了解如何在生成过程中使用 MSBuild 自动生成 REST API 客户端。 你将使用 [NSwag](/aspnet/core/tutorials/getting-started-with-nswag?tabs=visual-studio)，它是一种用于为 REST API 生成客户端代码的工具。

可在 GitHub 上的 .NET 示例存储库中的 [REST API 客户端生成](https://github.com/dotnet/samples/tree/main/msbuild/rest-api-client-generation)中找到完整示例代码。

该示例演示了一个使用公共[宠物店 API](https://petstore.swagger.io) 的控制台应用，该应用发布了 [OpenAPI 规范](https://petstore.swagger.io/v2/swagger.json)。

本教程假定 MSBuild 术语（如任务、目标、属性或运行时）的基本知识；有关必要的背景，请参阅 [MSBuild 概念](msbuild-concepts.md)一文。

当你希望在生成过程中运行命令行工具时，有两种方法可以考虑。 一种方法是使用 MSBuild [Exec 任务](exec-task.md)，这允许你运行命令行工具并指定其参数。 另一种方法是创建派生自 [ToolTask](xref:Microsoft.Build.Utilities.ToolTask) 的自定义任务，从而加强控制。

## <a name="prerequisites"></a>先决条件

你应了解任务、目标和属性等 MSBuild 概念。 请参阅 [MSBuild 概念](msbuild-concepts.md)。

这些示例需要 MSBuild，它随 Visual Studio 一起安装，但也可以单独安装。 请参阅[下载 MSBuild 而不下载 Visual Studio](https://visualstudio.microsoft.com/downloads/?q=build+tools)。

## <a name="option-1-exec-task"></a>选项 1：Exec 任务

[Exec 任务](/dotnet/api/microsoft.build.tasks.exec)仅使用指定的参数调用指定的进程，等待其完成，然后如果成功完成该进程则返回 `true`，如果发生错误则返回 `false`。

可以从 MSBuild 使用 NSwag 代码生成；请参阅 [NSwag.MSBuild](https://github.com/RicoSuter/NSwag/wiki/NSwag.MSBuild)。

完整的代码位于 PetReaderExecTaskExample 文件夹中；可以进行下载和查看。 在本教程中，你将完成分步教程并了解相关概念。

1. 创建名为 `PetReaderExecTaskExample` 的新控制台应用程序。 使用 .NET 6.0 或更高版本。

1. 在同一解决方案中创建另一个项目：`PetShopRestClient`（此解决方案将要包含生成的客户端作为库）。 对于此项目，请使用 .NET Standard 2.1。 生成的客户端不在 .NET Standard 2.0 上进行编译。

1. 在 `PetReaderExecTaskExample` 项目中，将项目依赖项添加到 `PetShopRestClient` 项目。

1. 在 `PetShopRestClient` 项目中，包括以下 NuGet 包：

   - Nswag.MSBuild，它允许从 MSBuild 访问代码生成器
   - Newtonsoft.Json，编译生成的客户端时需要
   - System.ComponentModel.Annotations，编译生成的客户端时需要

1. 在 `PetShopRestClient` 项目中，为代码生成添加一个文件夹（名为 `PetShopRestClient`）并删除自动生成的 Class1.cs。

1. 在项目的根目录中，创建一个名为 petshop-openapi-spec.json 的文本文件。 从[此处](https://petstore.swagger.io/v2/swagger.json)复制 OpenApi 规范，并将其保存在文件中。 最好复制规范的快照，而不是在生成过程中联机读取。 始终需要仅依赖于输入的持续可重现生成。 直接使用 API 可能会将今天工作的生成转换为明天从同一源失败的生成。 在 petshop-openapi-spec.json 上保存的快照将允许我们仍有即使规范发生更改也会生成的版本。

1. 接下来，修改 PetShopRestClient.csproj 并添加 [MSBuild 目标](msbuild-targets.md)以在生成过程中生成客户端。

   首先，添加一些适用于客户端生成的属性：

   ```xml
    <PropertyGroup>
        <PetOpenApiSpecLocation>petshop-openapi-spec.json</PetOpenApiSpecLocation>
        <PetClientClassName>PetShopRestClient</PetClientClassName>
        <PetClientNamespace>PetShopRestClient</PetClientNamespace>
        <PetClientOutputDirectory>PetShopRestClient</PetClientOutputDirectory>
    </PropertyGroup>
   ```

   添加以下目标：

   ```xml
    <Target Name="generatePetClient" BeforeTargets="CoreCompile" Inputs="$(PetOpenApiSpecLocation)" Outputs="$(PetClientOutputDirectory)\$(PetClientClassName).cs">
        <Exec Command="$(NSwagExe) openapi2csclient /input:$(PetOpenApiSpecLocation)  /classname:$(PetClientClassName) /namespace:$(PetClientNamespace) /output:$(PetClientOutputDirectory)\$(PetClientClassName).cs" ConsoleToMSBuild="true">
        <Output TaskParameter="ConsoleOutput" PropertyName="OutputOfExec" />
      </Exec>
    </Target>
    <Target Name="forceReGenerationOnRebuild" AfterTargets="CoreClean">
       <Delete Files="$(PetClientOutputDirectory)\$(PetClientClassName).cs"></Delete>
    </Target>
   ```

   请注意，此目标使用属性 [BeforeTarget 和 AfterTarget](target-build-order.md#beforetargets-and-aftertargets) 作为定义生成顺序的方式。 名为 `generatePetClient` 的第一个目标将在核心编译目标之前执行，因此在编译器执行之前将创建源。 输入参数和输出参数与[增量生成](how-to-build-incrementally.md)相关。 MSBuild 可将输入文件的时间戳和输出文件的时间戳进行比较，并确定是跳过、生成还是部分重新生成某个目标。

   在项目中安装 `NSwag.MSBuild` NuGet 包后，可以使用 `.csproj` 文件中的变量 `$(NSwagExe)` 在 MSBuild 目标中运行 NSwag 命令行工具。 这样一来，就可以通过 NuGet 轻松更新工具。 在这里，你将使用 `Exec` MSBuild 任务，通过生成客户端 Rest API 所需的参数来执行 NSwag 程序。 请参阅 [NSwag 命令和参数](https://github.com/RicoSuter/NSwag/wiki/NSwag.MSBuild)。

   可以通过将 `ConsoleToMsBuild="true"` 添加到 `<Exec>` 标记并使用 `<Output>` 标记中的 `ConsoleOutput` 参数捕获输出，从 `<Exec>` 中捕获输出。 `ConsoleOutput` 以 `Item` 的形式返回输出。 将剪裁掉空格。 当 `ConsoleToMSBuild` 为 true 时，将启用 `ConsoleOutput`。

   名为 `forceReGenerationOnRebuild` 的第二个目标将在清理过程中删除生成的类，以在重新生成目标执行期间强制重新生成已生成的代码。 此目标在 `CoreClean` MSBuild 预定义目标之后运行。

1. 执行 Visual Studio 解决方案重新生成，并查看在 `PetShopRestClient` 文件夹上生成的客户端。

1. 现在，请使用生成的客户端。 转到客户端 Program.cs，并复制以下代码：

   ```csharp
   using System;
   using System.Net.Http;

   namespace PetReaderExecTaskExample
   {
      internal class Program
      {
          private const string baseUrl = "https://petstore.swagger.io/v2";
          static void Main(string[] args)
          {
              HttpClient httpClient = new HttpClient();
              httpClient.BaseAddress = new Uri(baseUrl);
              var petClient = new PetShopRestClient.PetShopRestClient(httpClient);
              var pet = petClient.GetPetByIdAsync(1).Result;
              Console.WriteLine($"Id: {pet.Id} Name: {pet.Name} Status: {pet.Status} CategoryName: {pet.Category.Name}");
          }
      }
   }
   ```

   >[!NOTE]
   > 此代码使用 `new HttpClient()` 的原因是它易于演示，但它不是实际代码的最佳做法。 最佳做法是使用 `HttpClientFactory` 创建 `HttpClient` 对象，用于解决 `HttpClient` 请求的已知问题（例如资源耗尽或过时 DNS 问题）。 请参阅[使用 IHttpClientFactory 实现复原 HTTP 请求](/dotnet/architecture/microservices/implement-resilient-applications/use-httpclientfactory-to-implement-resilient-http-requests)。

恭喜！ 现在，你可以执行程序以了解其工作原理。

## <a name="option-2-custom-task-derived-from-tooltask"></a>选项 2：派生自 ToolTask 的自定义任务

在许多情况下，使用 `Exec` 任务就足以执行外部工具来进行诸如 REST API 客户端代码生成之类的操作，但如果你希望仅在不将绝对 Windows 路径用作输入时允许 REST API 客户端代码生成，该怎么办？ 或者，如果需要在可执行文件所在的位置中进行计算，该怎么办？ 如果在任何情况下都需要执行一些代码来执行额外的工作，则 [MSBuild 工具任务](/dotnet/api/microsoft.build.utilities.tooltask)是最佳解决方案。 `ToolTask` 类是派生自 MSBuild `Task` 的抽象类。 可以定义一个具体的子类，用于创建自定义 MSBuild 任务。 利用此方法，可以运行准备执行命令所需的任何代码。 应该先阅读教程[创建用于代码生成的自定义任务](tutorial-custom-task-code-generation.md)。

你将创建一个派生自 [MSBuild ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 的自定义任务，该任务将生成 REST API 客户端，但如果你尝试使用 http 地址引用 OpenApi 规范，它将设计为发出错误。 NSwag 支持 http 地址作为 OpenApi 规范输入，但出于本示例的目的，我们假设有一个设计要求禁止这样做。

完整的代码位于此 `PetReaderToolTaskExample` 文件夹中；可以进行下载和查看。 在本教程中，你将完成分步教程并了解可适用于你自己的方案的一些概念。

1. 为自定义任务创建新的 Visual Studio 项目。 将其称为 `RestApiClientGenerator` 并结合使用类库 (C#) 模板和 .NET Standard 2.0。 将解决方案命名为 `PetReaderToolTaskExample`。

1. 删除自动生成的 Class1.cs。

1. 添加 `Microsoft.Build.Utilities.Core` NuGet 包：

   - 创建名为 `RestApiClientGenerator` 的类
   - 从 MSBuild `ToolTask` 继承并实现抽象方法，如以下代码所示：

     ```csharp
     using Microsoft.Build.Utilities;

     namespace RestApiClientGenerator
     {
         public class RestApiClientGenerator : ToolTask
         {
             protected override string ToolName => throw new System.NotImplementedException();
 
             protected override string GenerateFullPathToTool()
             {
                 throw new System.NotImplementedException();
             }
         }
     }
     ```

1. 添加以下参数：

   - InputOpenApiSpec，规范所在位置
   - ClientClassName，所生成类的名称
   - ClientNamespaceName，生成类的命名空间
   - FolderClientClass，类所在的文件夹的路径
   - NSwagCommandFullPath，NSwag.exe 所在目录的完整路径

   ```csharp
        [Required]
        public string InputOpenApiSpec { get; set; }
        [Required]
        public string ClientClassName { get; set; }
        [Required]
        public string ClientNamespaceName { get; set; }
        [Required]
        public string FolderClientClass { get; set; }
        [Required]
        public string NSwagCommandFullPath { get; set; }
   ```

1. 安装 [NSwag 命令行工具](https://github.com/RicoSuter/NSwag/releases)。 你将需要 NSwag.exe 所在目录的完整路径。

1. 实现抽象方法：

   ```csharp
      protected override string ToolName => "RestApiClientGenerator";

      protected override string GenerateFullPathToTool()
      {
          return $"{NSwagCommandFullPath}\\NSwag.exe";
      }
   ```

1. 可以重写的方法有很多。 对于当前实现，请定义以下两个：

   - 定义命令参数：

    ```csharp
      protected override string GenerateCommandLineCommands()
      {
          return $"openapi2csclient /input:{InputOpenApiSpec}  /classname:{ClientClassName} /namespace:{ClientNamespaceName} /output:{FolderClientClass}\\{ClientClassName}.cs";
      }
    ```

   - 参数验证：

    ```csharp
    protected override bool ValidateParameters()
    {
          //http address is not allowed
          var valid = true;
          if (InputOpenApiSpec.StartsWith("http:") || InputOpenApiSpec.StartsWith("https:"))
          {
              valid = false;
              Log.LogError("URL is not allowed");
          }

          return valid;
    }
    ```

    > [!NOTE]
    > 此简单验证可以通过其他方式在 MSBuild 文件上完成，但建议在 C# 代码中执行此操作，并封装命令和逻辑。

1. 生成项目。

## <a name="create-a-console-app-to-use-the-new-msbuild-task"></a>创建控制台应用以使用新的 MSBuild 任务

下一步是创建使用该任务的应用。

1. 创建控制台应用项目，并将其称为 `PetReaderToolTaskConsoleApp`。 选择 .NET 6.0。 将其标记为启动项目。

1. 创建类库项目以生成名为 `PetRestApiClient` 的代码。  使用 .NET Standard 2.1。

1. 在 `PetReaderToolTaskConsoleApp` 项目中，创建到 `PetRestApiClient` 的项目依赖项。

1. 在 `PetRestApiClient` 项目中，创建文件夹 `PetRestApiClient`。 此文件夹将包含生成的代码。

1. 删除自动生成的 Class1.cs。

1. 在 `PetRestApiClient` 上，添加以下 NuGet 包：

   - Newtonsoft.Json，编译生成的客户端时需要
   - System.ComponentModel.Annotations，编译生成的客户端时需要

1. 在 `PetRestApiClient` 项目中，创建名为 petshop-openapi-spec.json 的文本文件（在项目文件夹中）。 若要添加 OpenApi 规范，请将内容从[此处](https://petstore.swagger.io/v2/swagger.json)复制到文件中。 我们喜欢仅依赖于输入的可重现生成，如前所述。 在本示例中，如果用户选择 URL 作为 OpenApi 规范输入，则将引发生成错误。

   > [!IMPORTANT]
   > 常规重新生成不起作用。 你将看到错误，指示无法复制或删除 `RestApiClientGenerator`.dll'。 这是因为正在尝试在使用它的同一个生成过程中生成 MBuild 自定义任务。 选择 `PetReaderToolTaskConsoleApp` 并仅重新生成该项目。 另一种解决方案是像在[教程：创建自定义任务](tutorial-custom-task-code-generation.md)示例中一样，将自定义任务放在完全独立的 Visual Studio 解决方案中。

1. 将以下代码复制到 Program.cs 中：

   ```csharp
    using System;
    using System.Net.Http;
    namespace PetReaderToolTaskConsoleApp
    {
      internal class Program
      {
          private const string baseUrl = "https://petstore.swagger.io/v2";
          static void Main(string[] args)
          {
              HttpClient httpClient = new HttpClient();
              httpClient.BaseAddress = new Uri(baseUrl);
              var petClient = new PetRestApiClient.PetRestApiClient(httpClient);
              var pet = petClient.GetPetByIdAsync(1).Result;
              Console.WriteLine($"Id: {pet.Id} Name: {pet.Name} Status: {pet.Status} CategoryName: {pet.Category.Name}");
          }
      }
    }
   ```

1. 更改 MSBuild 说明以调用任务并生成代码。 按照以下步骤编辑 PetRestApiClient.csproj：

   1. 注册 MSBuild 自定义任务的使用：

       ```xml
       <UsingTask TaskName="RestApiClientGenerator.RestApiClientGenerator" AssemblyFile="..\RestApiClientGenerator\bin\Debug\netstandard2.0\RestApiClientGenerator.dll" />
       ```

   1. 添加执行任务所需的一些属性：

      ```xml
       <PropertyGroup>
          <!--The place where the OpenApi spec is in-->
         <PetClientInputOpenApiSpec>petshop-openapi-spec.json</PetClientInputOpenApiSpec>
         <PetClientClientClassName>PetRestApiClient</PetClientClientClassName>
         <PetClientClientNamespaceName>PetRestApiClient</PetClientClientNamespaceName>
         <PetClientFolderClientClass>PetRestApiClient</PetClientFolderClientClass>
         <!--The directory where NSawg.exe is in-->
         <NSwagCommandFullPath>C:\Nsawg\Win</NSwagCommandFullPath>
        </PropertyGroup>
      ```

      > [!IMPORTANT]
      > 根据系统上的安装位置选择正确的 `NSwagCommandFullPath` 值。

   1. 添加 [MSBuild 目标](msbuild-targets.md)以在生成过程中生成客户端。 此目标应在 `CoreCompile` 执行之前执行，以生成编译中使用的代码。

      ```xml
      <Target Name="generatePetClient" BeforeTargets="CoreCompile" Inputs="$(PetClientInputOpenApiSpec)" Outputs="$(PetClientFolderClientClass)\$(PetClientClientClassName).cs">
        <!--Calling our custom task derivated from MSBuild Tool Task-->
        <RestApiClientGenerator InputOpenApiSpec="$(PetClientInputOpenApiSpec)" ClientClassName="$(PetClientClientClassName)" ClientNamespaceName="$(PetClientClientNamespaceName)" FolderClientClass="$(PetClientFolderClientClass)" NSwagCommandFullPath="$(NSwagCommandFullPath)"></RestApiClientGenerator>
      </Target>

      <Target Name="forceReGenerationOnRebuild" AfterTargets="CoreClean">
        <Delete Files="$(PetClientFolderClientClass)\$(PetClientClientClassName).cs"></Delete>
      </Target>
      ```

     `Input` 和 `Output` 与[增量生成](how-to-build-incrementally.md)相关，`forceReGenerationOnRebuild` 目标将删除 `CoreClean` 之后生成的文件，这将在重新生成操作期间强制重新生成客户端。

1. 选择 `PetReaderToolTaskConsoleApp` 并仅重新生成该项目。 现在，将生成客户端代码并编译代码。 可以执行它，并了解其工作原理。 此代码从文件生成代码，这是允许的。

1. 在此步骤中，你将演示参数验证。 在 PetRestApiClient.csproj 中，更改 `$(PetClientInputOpenApiSpec)` 属性以使用 URL：

   ```xml
     <PetClientInputOpenApiSpec>https://petstore.swagger.io/v2/swagger.json</PetClientInputOpenApiSpec>
   ```

1. 选择 `PetReaderToolTaskConsoleApp` 并仅重新生成该项目。 根据设计要求，你将收到错误“不允许使用 URL”。

## <a name="download-the-code"></a>下载代码

安装 [NSwag 命令行工具](https://github.com/RicoSuter/NSwag/releases)。 然后，你将需要 NSwag.exe 所在目录的完整路径。 之后，编辑 PetRestApiClient.csproj，并基于计算机上的安装路径选择正确的 `$(NSwagCommandFullPath)` 值。 现在，选择 `RestApiClientGenerator` 并仅生成该项目，最后选择并重新生成 `PetReaderToolTaskConsoleApp`。 可以执行 `PetReaderToolTaskConsoleApp`。 用于验证一切按预期运行。

## <a name="next-steps"></a>后续步骤

你可能希望将自定义任务发布为 NuGet 包。

> [!div class="nextstepaction"]
> [教程：创建自定义任务](tutorial-custom-task-code-generation.md#package-the-task-for-distribution)

或者，了解如何测试自定义任务。

> [!div class="nextstepaction"]
> [测试自定义 MSBuild 任务](tutorial-test-custom-task.md)