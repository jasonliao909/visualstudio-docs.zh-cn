---
title: 将 Visual Studio 生成工具安装到容器
titleSuffix: ''
description: 了解如何将 Visual Studio 生成工具安装到 Windows 容器，以支持持续集成和持续交付 (CI/CD) 工作流。
ms.date: 06/09/2021
ms.topic: conceptual
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: d6208ae736b01c13a9666b67fe694743d2421d1e
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129430555"
---
# <a name="install-build-tools-into-a-container"></a>将生成工具安装到容器

可以将 Visual Studio 生成工具安装到 Windows 容器，用于支持持续集成和持续交付 (CI/CD) 工作流。 本文将指导你完成所需的 Docker 配置更改以及可以在容器中安装的[工作负荷和组件](workload-component-id-vs-build-tools.md)。

对于包装不仅可以在 CI/CD 服务器环境中使用，而且可以用于开发环境的一致的生成系统，[容器](https://www.docker.com/what-container)是一种好方法。 例如，可以将源代码装载到要由自定义环境生成的容器中，同时继续使用 Visual Studio 或其他工具编写代码。 如果 CI/CD 工作流使用相同容器映像，则可以确信代码会以一致的方式生成。 还可以使用容器来实现运行时一致性，这对于将多个容器与业务流程系统一起使用的微服务十分常见，但不在本文的讨论范围内。

如果 Visual Studio 生成工具没有生成源代码所需的内容，则可以将这些相同步骤用于其他 Visual Studio 产品。 但是请注意，Windows 容器不支持交互用户界面，因此所有命令都必须自动执行。

## <a name="before-you-begin"></a>在开始之前

下面假定你对 [Docker](https://www.docker.com/what-docker) 比较熟悉。 如果你尚不熟悉在 Windows 上运行 Docker，请了解如何[在 Windows 上安装和配置 Docker 引擎](/virtualization/windowscontainers/manage-docker/configure-docker-daemon)。

下面的基础映像是一个示例，可能不适用于你的系统。 请阅读 [Windows 容器版本兼容性](/virtualization/windowscontainers/deploy-containers/version-compatibility)，以确定应将哪个基础映像用于你的环境。

## <a name="create-and-build-the-dockerfile"></a>创建和生成 Dockerfile

将下面的示例 Dockerfile 保存为磁盘上的新文件。 如果该文件仅仅命名为“Dockerfile”，则默认情况下会识别它。

> [!WARNING]
> 此示例 Dockerfile 只排除无法安装到容器的旧版 Windows SDK。 较旧版本会导致生成命令失败。

1. 打开命令提示。

1. 创建新目录（推荐）：

   ```shell
   mkdir C:\BuildTools
   ```

1. 将目录更改为此新目录：

   ```shell
   cd C:\BuildTools
   ```

1. 将以下内容保存到 C:\BuildTools\Dockerfile。
 
   ::: moniker range="vs-2017"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.7.2.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   RUN `
       # Download the Build Tools bootstrapper.
       curl -SL --output vs_buildtools.exe https://aka.ms/vs/15/release/vs_buildtools.exe `
       `
       # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
       && (start /w vs_buildtools.exe --quiet --wait --norestart --nocache `
           --installPath C:\BuildTools `
           --add Microsoft.VisualStudio.Workload.AzureBuildTools `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
           --remove Microsoft.VisualStudio.Component.Windows81SDK `
           || IF "%ERRORLEVEL%"=="3010" EXIT 0) `
       `
       # Cleanup
       && del /q vs_buildtools.exe

   # Define the entry point for the Docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > 有关工作负载和组件的列表，请参阅 [Visual Studio 生成工具组件目录](workload-component-id-vs-build-tools.md)。
   >

   > [!WARNING]
   > 如果映像直接基于 microsoft/windowsservercore 或 mcr.microsoft.com/windows/servercore（请参阅 [Microsoft 将联合容器目录](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/)），可能无法正确安装 .NET Framework，且不会指示任何安装错误。 安装完成后，可能无法运行托管代码。 相反，可使映像以 [microsoft/dotnet-framework:4.7.2](https://hub.docker.com/r/microsoft/dotnet-framework) 或更高版本为基础。 另请注意，标记为 4.7.2 或更高版本的映像可能使用 PowerShell 作为默认 `SHELL`，这将导致 `RUN` 和 `ENTRYPOINT` 指令失败。
   >
   > Visual Studio 2017 版本 15.8 或更高版本（任何产品）无法在 mcr.microsoft.com/windows/servercore:1809 或更高版本上正常安装。 不显示任何错误信息。
   >
   > 请参阅 [Windows 容器版本兼容性](/virtualization/windowscontainers/deploy-containers/version-compatibility)，以了解哪些主机操作系统版本支持哪些容器操作系统版本，并请参阅[容器的已知问题](build-tools-container-issues.md)了解已知问题。
   
   ::: moniker-end

   ::: moniker range="vs-2019"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.8.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   RUN `
       # Download the Build Tools bootstrapper.
       curl -SL --output vs_buildtools.exe https://aka.ms/vs/16/release/vs_buildtools.exe `
       `
       # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
       && (start /w vs_buildtools.exe --quiet --wait --norestart --nocache modify `
           --installPath "%ProgramFiles(x86)%\Microsoft Visual Studio\2019\BuildTools" `
           --add Microsoft.VisualStudio.Workload.AzureBuildTools `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
           --remove Microsoft.VisualStudio.Component.Windows81SDK `
           || IF "%ERRORLEVEL%"=="3010" EXIT 0) `
       `
       # Cleanup
       && del /q vs_buildtools.exe

   # Define the entry point for the docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > 有关工作负载和组件的列表，请参阅 [Visual Studio 生成工具组件目录](workload-component-id-vs-build-tools.md)。
   >

   > [!WARNING]
   > 如果映像直接基于 microsoft/windowsservercore，可能无法正确安装 .NET Framework，且不会指示任何安装错误。 安装完成后，可能无法运行托管代码。 相反，可使映像以 [microsoft/dotnet-framework:4.8](https://hub.docker.com/r/microsoft/dotnet-framework) 或更高版本为基础。 另请注意，标记为 4.8 或更高版本的映像可能使用 PowerShell 作为默认 `SHELL`，这将导致 `RUN` 和 `ENTRYPOINT` 指令失败。
   >
   > 请参阅 [Windows 容器版本兼容性](/virtualization/windowscontainers/deploy-containers/version-compatibility)，以了解哪些主机操作系统版本支持哪些容器操作系统版本，并请参阅[容器的已知问题](build-tools-container-issues.md)了解已知问题。

   ::: moniker-end
   
   ::: moniker range=">=vs-2022"

   ```dockerfile
   # escape=`

   # Use the latest Windows Server Core image with .NET Framework 4.8.
   FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

   # Restore the default Windows shell for correct batch processing.
   SHELL ["cmd", "/S", "/C"]

   RUN `
       # Download the Build Tools bootstrapper.
       curl -SL --output vs_buildtools.exe https://aka.ms/vs/17/pre/vs_buildtools.exe `
       `
       # Install Build Tools with the Microsoft.VisualStudio.Workload.AzureBuildTools workload, excluding workloads and components with known issues.
       && (start /w vs_buildtools.exe --quiet --wait --norestart --nocache modify `
           --installPath "%ProgramFiles(x86)%\Microsoft Visual Studio\2022\BuildTools" `
           --add Microsoft.VisualStudio.Workload.AzureBuildTools `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10240 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.10586 `
           --remove Microsoft.VisualStudio.Component.Windows10SDK.14393 `
           --remove Microsoft.VisualStudio.Component.Windows81SDK `
           || IF "%ERRORLEVEL%"=="3010" EXIT 0) `
       `
       # Cleanup
       && del /q vs_buildtools.exe

   # Define the entry point for the docker container.
   # This entry point starts the developer command prompt and launches the PowerShell shell.
   ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2022\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", "&&", "powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]
   ```

   > [!TIP]
   > 有关工作负载和组件的列表，请参阅 [Visual Studio 生成工具组件目录](workload-component-id-vs-build-tools.md)。
   >

   > [!WARNING]
   > 如果映像直接基于 microsoft/windowsservercore，可能无法正确安装 .NET Framework，且不会指示任何安装错误。 安装完成后，可能无法运行托管代码。 相反，可使映像以 [microsoft/dotnet-framework:4.8](https://hub.docker.com/r/microsoft/dotnet-framework) 或更高版本为基础。 另请注意，标记为 4.8 或更高版本的映像可能使用 PowerShell 作为默认 `SHELL`，这将导致 `RUN` 和 `ENTRYPOINT` 指令失败。
   >
   > 请参阅 [Windows 容器版本兼容性](/virtualization/windowscontainers/deploy-containers/version-compatibility)，以了解哪些主机操作系统版本支持哪些容器操作系统版本，并请参阅[容器的已知问题](build-tools-container-issues.md)了解已知问题。

   ::: moniker-end
   > [!NOTE]
   > 错误代码 `3010` 用于在需要重新启动时指示成功，请参阅 [MsiExec.exe 错误消息](/windows/win32/msi/error-codes)了解详细信息。

1. 从该目录处运行以下命令。

   ::: moniker range="vs-2017"

   ```shell
   docker build -t buildtools2017:latest -m 2GB .
   ```

   此命令使用 2 GB 内存在当前目录中生成 Dockerfile。 安装某些工作负载后，默认的 1 GB 会不够用；你有可能只使用 1 GB 内存进行生成，具体取决于生成环境。

   最终映像带有标记“buildtools2017:latest”，因此你可以在作为“buildtools2017”的容器中轻松运行它因为如果未指定任何标记，则默认情况下使用“latest”标记。 如果要在更[高级的方案](advanced-build-tools-container.md)中使用特定版本的 Visual Studio 15 生成工具 2017加，则你可以改为使用特定 Visual Studio 生成号以及“latest”来标记容器，因此容器可以按一致方式使用特定版本。

   ::: moniker-end

   ::: moniker range="vs-2019"

   ```shell
   docker build -t buildtools2019:latest -m 2GB .
   ```

   此命令使用 2 GB 内存在当前目录中生成 Dockerfile。 安装某些工作负载后，默认的 1 GB 会不够用；你有可能只使用 1 GB 内存进行生成，具体取决于生成环境。

   最终映像带有标记“buildtools2019:latest”，因此可以在作为“buildtools2019”的容器中轻松运行它，因为如果未指定任何标记，默认情况下会使用“latest”标记。 如果要在更[高级的方案](advanced-build-tools-container.md)中使用特定版本的 Visual Studio 生成工具 2019，则可以改用特定 Visual Studio 生成号以及“latest”来标记容器，因此容器可以按一致方式使用特定版本。

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   ```shell
   docker build -t buildtools:latest -m 2GB .
   ```

   此命令使用 2 GB 内存在当前目录中生成 Dockerfile。 安装某些工作负载后，默认的 1 GB 会不够用；你有可能只使用 1 GB 内存进行生成，具体取决于生成环境。

   最终映像带有标记“buildtools:latest”，因此可以在作为“buildtools”的容器中轻松运行它，因为如果未指定任何标记，默认情况下会使用“latest”标记。 如果要在更[高级的方案](advanced-build-tools-container.md)中使用特定版本的 Visual Studio 生成工具，则可以改用特定 Visual Studio 生成号以及“latest”来标记容器，因此容器可以按一致方式使用特定版本。

   ::: moniker-end

## <a name="using-the-built-image"></a>使用生成的映像

现在已创建了映像，可以在容器中运行它以进行交互式自动生成。 该示例使用开发人员命令提示，因此已配置了 PATH 和其他环境变量。

1. 打开命令提示。

1. 运行容器以启动 PowerShell 环境（设置了所有开发人员环境变量）：

   ::: moniker range="vs-2017"

   ```shell
   docker run -it buildtools2017
   ```

   ::: moniker-end

   ::: moniker range="vs-2019"

   ```shell
   docker run -it buildtools2019
   ```

   ::: moniker-end

   ::: moniker range=">=vs-2022"

   ```shell
   docker run -it buildtools
   ```

   ::: moniker-end

若要将此映像用于 CI/CD 工作流，可以将它发布到自己的 [Azure 容器注册表](https://azure.microsoft.com/services/container-registry)或其他内部 [Docker 注册表](https://docs.docker.com/registry/deploying)，这样服务器只需拉取它即可。

   > [!NOTE]
   > 如果 Docker 容器无法启动，则可能出现了 Visual Studio 安装问题。 可以更新 Dockerfile 以删除调用 Visual Studio 批处理命令的步骤。 这样，可以启动 Docker 容器并读取安装错误日志。
   >
   > 在 Dockerfile 文件中，删除 `ENTRYPOINT` 命令中的 `C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` 和 `&&` 参数。 现在，该命令应为 `ENTRYPOINT ["powershell.exe", "-NoLogo", "-ExecutionPolicy", "Bypass"]`。 接下来，重新生成 Dockerfile 并执行 `run` 命令以访问容器文件。 要找到安装错误日志，请转到 `$env:TEMP` 目录并找到 `dd_setup_<timestamp>_errors.log` 文件。
   >
   > 确定安装问题并进行修复后，可以将 `C:\\BuildTools\\Common7\\Tools\\VsDevCmd.bat` 和 `&&` 参数添加回 `ENTRYPOINT` 命令并重新生成 Dockerfile。
   >
   > 有关详细信息，请参阅[容器的已知问题](build-tools-container-issues.md)。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>请参阅

* [容器的高级示例](advanced-build-tools-container.md)
* [容器的已知问题](build-tools-container-issues.md)
* [Visual Studio 生成工具工作负载和组件 ID](workload-component-id-vs-build-tools.md)
