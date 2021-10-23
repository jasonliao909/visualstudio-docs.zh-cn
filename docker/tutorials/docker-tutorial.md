---
title: 教程：Windows 或 Mac 上的 Docker 和 Visual Studio Code 入门
description: 一个多步骤教程，其中介绍了配合使用 Docker 与 Visual Studio Code 的基础知识。
ms.date: 08/06/2021
author: nebuk89
ms.author: ghogen
manager: jmartens
ms.technology: vs-docker
ms.custom: contperf-fy22q1
ms.topic: tutorial
ms.workload:
- azure
next_page: app.md
ms.openlocfilehash: c4b1bd4a05c7c8a95a457c18be248cb40a0f94a2
ms.sourcegitcommit: efe1d737fd660cc9183177914c18b0fd4e39ba8b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2021
ms.locfileid: "130211449"
---
# <a name="tutorial-get-started-with-docker"></a>教程：Docker 入门

在本教程中，你将了解如何使用 Visual Studio Code 在 Windows 或 Mac 上创建和部署 Docker 应用，包括将多个容器与数据库结合使用，以及使用 Docker Compose。 还会将容器化应用部署到 Azure。

容器是精简的虚拟环境，如虚拟机 (VM)，提供用于生成和运行应用的平台，但没有完整操作系统的完整大小和开销。 [Docker](https://www.docker.com) 是一个行业标准的第三方容器提供程序和容器管理系统。 Docker Desktop 在计算机上运行，并管理本地容器。 Visual Studio 和 VS Code 等开发工具提供了扩展，让你可以使用本地安装的 Docker Desktop 服务来创建容器化应用、将应用部署到容器，以及调试容器上运行的应用。

## <a name="prerequisites"></a>必备条件

- [Visual Studio Code](https://code.visualstudio.com/download)
- Docker Desktop（[Windows](https://docs.docker.com/docker-for-windows/install/) 或 [Mac](https://docs.docker.com/docker-for-mac/install/) 版）。

## <a name="start-the-tutorial"></a>开始教程

如果你已运行该命令来开始学习教程，恭喜！  如果没有，请打开命令提示符或 bash 窗口，并运行以下命令：

```cli
docker run -d -p 80:80 docker/getting-started
```

你会注意到使用了几个标志。 下面是关于它们的一些详细信息：

- `-d` - 在分离模式下（在后台）运行容器
- `-p 80:80` -将主机的端口 80 映射到容器中的端口 80
- `docker/getting-started` - 要使用的映像

> [!TIP]
> 可以组合单字符标志以缩短整个命令。
> 例如，可将上述命令编写为：
>
> ```cli
> docker run -dp 80:80 docker/getting-started
> ```

## <a name="the-vs-code-extension"></a>VS Code 扩展

在深入探讨之前，这里要重点介绍一下 Docker VS Code 扩展，它使你能够快速查看计算机上运行的容器。 通过该扩展，你可以快速访问容器日志，可以在容器中获取 shell，并能够轻松管理容器生命周期（停止、删除等）。

若要访问该扩展，请按照[此处](https://code.visualstudio.com/docs/containers/overview)的说明进行操作。 使用左侧的 Docker 图标打开 Docker 视图。 如果现在打开扩展，你将看到此教程正在运行！ 容器名称（下述 `angry_taussig`）是随机创建的名称。 因此，你很可能会有不同的名称。

![在 Docker 扩展中运行的教程容器](media/vs-tutorial-in-extension.png)

## <a name="what-is-a-container"></a>什么是容器

现在你已运行了一个容器，什么是容器？ 简而言之，容器就是计算机上的另一个进程，并与主机上的所有其他进程隔离。 这种隔离利用了[内核命名空间和 cgroup](https://medium.com/@saschagrunert/demystifying-containers-part-i-kernel-space-2c53d6979504)，这些功能已在 Linux 中存在很长时间。 Docker 一直在努力使这些功能易于访问和使用。

> [!NOTE]
> **从头开始创建容器** 如果你想了解如何从头开始构建容器，可观看 Aqua Security 的 Liz Rice 的一个视频，她在该视频中使用 Go 从头开始创建容器：
>
> [!VIDEO https://www.youtube-nocookie.com/embed/8fi7uSYlOdc]

## <a name="what-is-a-container-image"></a>什么是容器映像

运行容器时，它使用独立的文件系统。 此自定义文件系统由一个容器映像提供。 由于映像包含容器的文件系统，因此它必须包含运行应用程序所需的所有内容 - 所有依赖项、配置、脚本、二进制文件等。 映像还包含容器的其他配置，例如环境变量、要运行的默认命令以及其他元数据。

稍后我们将深入探讨映像，包括分层、最佳做法等主题。

> [!NOTE]
> 如果你熟悉 `chroot`，可将容器看作 `chroot` 的扩展版本。 文件系统完全源自映像。 但是，容器还添加了其他隔离，如果只使用 chroot，是不可用的。

## <a name="next-steps"></a>后续步骤

继续学习教程！

> [!div class="nextstepaction"]
> [应用程序](your-application.md)
