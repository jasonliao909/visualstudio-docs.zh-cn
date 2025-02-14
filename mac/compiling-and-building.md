---
title: 编译和生成
description: 本文介绍如何在 Visual Studio for Mac 中编译和生成项目和解决方案
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 03/03/2022
ms.custom: devdivchpfy22
ms.topic: how-to
ms.assetid: FB253757-DB00-4889-A6BF-E44722E25BD1
ms.openlocfilehash: 352a0da0c88a0668707a0998d0421f49f26fe4ca
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144476047"
---
# <a name="compiling-and-building-in-visual-studio-for-mac"></a>在 Visual Studio for Mac 中编译和生成

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

Visual Studio for Mac 可用于在项目开发过程中生成应用程序和创建程序集。 经常生成代码非常重要，这样可以快速识别类型不匹配、错误语法、拼写错误的关键字以及其他编译时错误。 通过生成并调试，还可以查找并修复运行时错误，例如逻辑、IO 和被零除错误。

成功的生成意味着源代码包含正确的语法，并且可以解析对库、程序集和其他组件的所有静态引用。 生成过程将生成一个应用程序可执行文件。 然后，可以通过调试和不同类型的手动和自动测试来测试此可执行文件，以验证代码质量。 应用程序经过完全测试后，可以编译一个发布版本以部署到客户。

在 Mac 上，可以使用以下任一方法来生成应用程序：Visual Studio for Mac、MSBuild 命令行工具，或 Azure Pipelines。


|生成方法  |优点  |
|---------|---------|
|Visual Studio for Mac     |  - 立即创建生成并在调试程序中对其进行测试。<br />- 运行 C# 项目的多处理器生成。<br />- 自定义生成系统的不同方面。        |
|MSBuild 命令行     |   - 无需安装Visual Studio for Mac即可生成项目。<br />- 为所有项目类型运行多处理器生成。<br />- 自定义生成系统的大部分区域。  |
|Azure Pipelines     |   - 在持续集成/持续交付管道中自动执行生成过程。<br />- 将自动测试应用于每个生成。 <br />- 为生成过程采用几乎无限的基于云的资源。<br />- 修改生成工作流，并创建生成活动以执行深层的自定义任务。 |

本节中的文档将详细介绍基于 IDE 的生成过程。 若要在不安装 Visual Studio for Mac 的情况下通过命令行生成应用程序，则可以安装最新的 [.NET Core SDK](https://dotnet.microsoft.com/download)。 有关通过命令行生成应用程序的详细信息，请参阅 [MSBuild](/visualstudio/msbuild/msbuild)。 有关使用 Azure Pipelines 生成应用程序的详细信息，请参阅 [Azure Pipelines](/azure/devops/pipelines)。


> [!NOTE]
> 本主题适用于 Visual Studio for Mac。 对于 Windows 上的 Visual Studio，请参阅 [Visual Studio 中的编译和生成](/visualstudio/ide/compiling-and-building-in-visual-studio)。


## <a name="building-from-the-ide"></a>从 IDE 生成

使用 Visual Studio for Mac，可立即创建和运行生成，并保持对生成功能的控制。 创建项目时，Visual Studio for Mac 会定义用于为生成设置上下文的默认生成配置。 可以编辑默认生成配置，还可以创建自己的生成配置。 创建或修改这些配置会自动更新项目文件，之后 MSBuild 会使用该文件生成项目。

有关如何在 IDE 中生成项目和解决方案的详细信息，请参阅[生成和清理项目和解决方案](building-and-cleaning-projects-and-solutions.md)指南。

Visual Studio for Mac还可用于：

* 通过编辑Project的选项更改输出路径：

    ![更改输出路径](media/compiling-and-building-image4.png)

* 更改生成输出的详细级别：

    ![更改生成的详细级别](media/compiling-and-building-image5.png)

* 在生成或清理之前、之后或者生成或清理过程中添加自定义命令：

    ![添加自定义命令](media/compiling-and-building-image6.png)


## <a name="see-also"></a>请参阅

- [编译和生成（Windows 上的 Visual Studio）](/visualstudio/ide/compiling-and-building-in-visual-studio)
