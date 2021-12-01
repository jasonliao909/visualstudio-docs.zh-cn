---
title: Docker Compose 生成设置
author: ghogen
description: 了解如何编辑 Docker Compose 生成属性以自定义 Visual Studio 生成和运行 Docker Compose 应用程序的方式。
ms.custom: SEO-VS-2020
ms.author: ghogen
ms.date: 04/06/2021
ms.technology: vs-container-tools
ms.topic: reference
ms.openlocfilehash: b541568567d7af7002ecf576700099fec1aeb2d7
ms.sourcegitcommit: ff81d69902e869b227d9ceb6e95023d1c63425b1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129595126"
---
# <a name="docker-compose-build-properties"></a>Docker Compose 生成属性

除了用于控制各个 Docker 项目的属性（如[容器工具生成属性](container-msbuild-properties.md)中所述），还可以通过设置 MSBuild 用于生成解决方案的 Docker Compose 属性来自定义 Visual Studio 生成 Docker Compose 项目的方式。 还可以通过设置 Docker Compose 配置文件中的文件标签来控制 Visual Studio 调试程序运行 Docker Compose 应用的方式。

## <a name="how-to-set-the-msbuild-properties"></a>如何设置 MSBuild 属性

若要设置属性的值，请编辑项目文件。 对于 Docker Compose 属性，此项目文件是扩展名为 .dcproj 的文件，除非在下一部分的表中另有说明。 例如，假设要指定在开始调试时启动浏览器。 可以在 .dcproj 项目文件中设置 `DockerLaunchAction` 属性，如下所示。

```xml
<PropertyGroup>
   <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
</PropertyGroup>
```

可以向现有 `PropertyGroup` 元素添加属性设置，如果没有，则新建一个 `PropertyGroup` 元素。

## <a name="docker-compose-msbuild-properties"></a>Docker Compose MSBuild 属性

下表显示了可用于 Docker Compose 项目的 MSBuild 属性。

| 属性名称 | 位置 | 说明 | 默认值  |
|---------------|----------|-------------|----------------|
|AdditionalComposeFilePaths|dcproj|以分号分隔的列表指定要发送给 docker-compose.exe 供所有命令使用的其他撰写文件。 允许使用来自 docker-compose 项目文件 (dcproj) 的相对路径。|-|
|DockerComposeBaseFilePath|dcproj|执行 docker-compose 文件的文件名的第一部分，不带 .yml 扩展名  。 例如： <br>1. DockerComposeBaseFilePath = null/未定义：使用基础文件路径 docker-compose，文件将命名为 docker-compose.yml 和 docker-compose.override.yml。<br>2. DockerComposeBaseFilePath = mydockercompose：文件将命名为 mydockercompose.yml 和 mydockercompose.override.yml。<br> 3. DockerComposeBaseFilePath = ..\mydockercompose：文件将向上提升一级。 |docker-compose|
|DockerComposeBuildArguments|dcproj|指定要传递给 `docker-compose build` 命令的额外参数。 例如，`--parallel --pull`。 |
|DockerComposeDownArguments|dcproj|指定要传递给 `docker-compose down` 命令的额外参数。 例如，`--timeout 500`。|-|  
|DockerComposeProjectName| dcproj | 如果已指定，它将替代 docker-compose 项目的项目名称。 | dockercompose + 自动生成的哈希 |
|DockerComposeProjectPath|csproj 或 vbproj|Docker-compose 项目 (.dcproj) 文件的相对路径。 发布服务项目时设置此属性，以查找存储在 docker-compose.yml 文件中的关联映像生成设置。|-|
|DockerComposeProjectsToIgnore|dcproj| 指定在调试期间要被 docker-compose 工具忽略的项目。 此属性可用于任何项目。 可通过以下两种方式之一来指定文件路径： <br> 1. 相对于 dcproj。 例如，`<DockerComposeProjectsToIgnore>path\to\AngularProject1.csproj</DockerComposeProjectsToIgnore>`。 <br> 2. 绝对路径。<br> 注意：路径应由分隔符 `;` 分隔。|-|
|DockerComposeUpArguments|dcproj|指定要传递给 `docker-compose up` 命令的额外参数。 例如，`--timeout 500`。|-|
|DockerDevelopmentMode| dcproj | 控制是否在容器中生成用户项目。 可取值为“Fast”或“Regular”，用于控制在 Dockerfile 中[生成哪些阶段](https://aka.ms/containerfastmode)。 调试配置默认为“Fast”模式，否则为“Regular”模式。 | 快速 |
|DockerLaunchAction| dcproj | 指定要针对 F5 或 Ctrl+F5 执行的启动操作。  允许的值为 None、LaunchBrowser 和 LaunchWCFTestClient。 | None |
|DockerLaunchBrowser| dcproj | 指示是否启动浏览器。 如果指定了 DockerLaunchAction，则忽略。 | False |
|DockerServiceName| dcproj| 如果指定了 DockerLaunchAction 或 DockerLaunchBrowser，则 DockerServiceName 指定启动在 docker-compose 文件中引用的哪个服务。|-|
|DockerServiceUrl| dcproj | 启动浏览器时将使用的 URL。  有效的替换令牌为“{ServiceIPAddress}”、“{ServicePort}”和“{Scheme}”。  例如：{Scheme}://{ServiceIPAddress}:{ServicePort}|-|
|DockerTargetOS| dcproj | 生成 Docker 映像时使用的目标 OS。|-|

## <a name="example"></a>示例

如果通过将 `DockerComposeBaseFilePath` 设置为相对路径来更改 docker compose 文件的位置，则还需要确保更改生成上下文，以便其引用解决方案文件夹。 例如，如果 docker compose 文件是名为 DockerComposeFiles 的文件夹，则 docker compose 文件应将生成上下文设置为“..”或“../..”，具体取决于它相对于解决方案文件夹的位置  。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0" Sdk="Microsoft.Docker.Sdk">
  <PropertyGroup Label="Globals">
    <ProjectVersion>2.1</ProjectVersion>
    <DockerTargetOS>Windows</DockerTargetOS>
    <ProjectGuid>154022c1-8014-4e9d-bd78-6ff46670ffa4</ProjectGuid>
    <DockerLaunchAction>LaunchBrowser</DockerLaunchAction>
    <DockerServiceUrl>{Scheme}://{ServiceIPAddress}{ServicePort}</DockerServiceUrl>
    <DockerServiceName>webapplication1</DockerServiceName>
    <DockerComposeBaseFilePath>DockerComposeFiles\mydockercompose</DockerComposeBaseFilePath>
    <AdditionalComposeFilePaths>AdditionalComposeFiles\myadditionalcompose.yml</AdditionalComposeFilePaths>
  </PropertyGroup>
  <ItemGroup>
    <None Include="DockerComposeFiles\mydockercompose.override.yml">
      <DependentUpon>DockerComposeFiles\mydockercompose.yml</DependentUpon>
    </None>
    <None Include="DockerComposeFiles\mydockercompose.yml" />
    <None Include=".dockerignore" />
  </ItemGroup>
</Project>
```

mydockercompose.yml 文件应如下所示，其中生成上下文设置为解决方案文件夹的相对路径（在本例中为 `..`）  。

```yml
version: '3.4'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    build:
      context: ..
      dockerfile: WebApplication1\Dockerfile
```

> [!NOTE]
> DockerComposeBuildArguments、DockerComposeDownArguments 和 DockerComposeUpArguments 是 Visual Studio 2019 版本 16.3 中的新增内容。

## <a name="overriding-visual-studios-docker-compose-configuration"></a>替代 Visual Studio 的 Docker Compose 配置

通常 docker-compose.override.yml 用于替代 docker-compose.yml 中的某些设置 。 此外，Visual Studio 生成替代文件 docker-compose.vs.debug.g,yml（用于“Fast”模式）和 docker-compose.vs.release.g.yml（用于“Regular”模式）文件，这些文件中的设置专用于在 Visual Studio 中运行应用程序。 可以替代这些 Visual Studio 设置，具体方法是将名为 docker-compose.vs.debug.yml（对于“Fast”模式）或 docker-compose.vs.release.yml（对于“Regular”模式）的文件放置在与 docker-compose.yml 文件相同的目录中。 右键单击 docker-compose 项目并选择“打开文件资源管理器中的文件夹”，然后使用“添加” > “现有项”，将文件添加到 docker-compose 项目中。

>[!TIP] 
>若要找出任意 Visual Studio 设置的默认值，请查看 docker-compose.vs.debug.g.yml 或 docker-compose.vs.release.g.yml 的中间输出目录（例如，obj/Docker）。 这些文件由 Visual Studio 生成，不应进行修改。

### <a name="docker-compose-file-labels"></a>Docker Compose 文件标签

 在 docker-compose.vs.debug.yml 或 docker-compose.vs.release.yml 中，可以定义特定于替代的标签，如下所示：

```yml
services:
  webapplication1:
    labels:
      com.microsoft.visualstudio.debuggee.workingdirectory: "C:\\my_app_folder"
```

如前面的示例所示，用双引号将这些值括起来，并在路径中使用反斜杠作为转义字符。

|标签名称|描述|
|----------|-----------|
|com.microsoft.visualstudio.debuggee.arguments|开始调试时传递给程序的参数。 对于 .NET Core 应用，这些参数通常是 NuGet 包的其他搜索路径，后面是指向项目输出程序集的路径。|
|com.microsoft.visualstudio.debuggee.program|启动调试时启动的程序。 对于 .Net Core 应用，此设置通常为“dotnet”  。|
|com.microsoft.visualstudio.debuggee.workingdirectory|开始调试时用作起始目录的目录。 对于 Linux 容器，此设置通常为 /app；对于 Windows 容器，此设置通常为 C:\app   。|
|com.microsoft.visualstudio.debuggee.killprogram|此命令用于停止在容器中运行的调试对象程序（如有必要）。|

### <a name="customize-the-docker-build-process"></a>自定义 Docker 生成过程

通过在 `build` 属性中使用 `target` 设置，可以声明在 Dockerfile 中生成哪个阶段。 此替代只能在 docker-compose.vs.debug.yml 或 docker-compose.vs.release.yml 中使用。 

```yml
services:
  webapplication1:
    build:
      target: customStage
    labels:
      ...
```

### <a name="customize-the-app-startup-process"></a>自定义应用启动过程

在启动应用之前，可以通过使用 `entrypoint` 设置并使其依赖于 `DockerDevelopmentMode`，运行命令或自定义脚本。 例如，如果只需要在“Fast”模式下通过运行 `update-ca-certificates` 来创建证书，而不需要在“Regular”模式下这样做，则可以只在 docker-compose.vs.debug.yml 中添加以下代码：

```yml
services:
  webapplication1:
    entrypoint: "sh -c 'update-ca-certificates && tail -f /dev/null'"
    labels:
      ...
```

## <a name="next-steps"></a>后续步骤

有关 MSBuild 属性的一般信息，请参阅 [MSBuild 属性](../msbuild/msbuild-properties.md)。

## <a name="see-also"></a>请参阅

[容器工具生成属性](container-msbuild-properties.md)

[容器工具启动设置](container-launch-settings.md)

[管理 Visual Studio 中 Docker Compose 的启动配置文件](launch-profiles.md)

[MSBuild 保留属性和已知属性](../msbuild/msbuild-reserved-and-well-known-properties.md)
