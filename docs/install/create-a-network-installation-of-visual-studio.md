---
title: 创建基于网络的安装
description: 了解如何创建用于在企业中部署 Visual Studio 的网络安装点。
ms.date: 3/3/2022
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 4CABFD20-962E-482C-8A76-E4012052F701
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 00abfc62b72f46b5671c99af0a860c8f63262d5e
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139548868"
---
# <a name="create-maintain-and-deploy-a-network-installation-of-visual-studio"></a>创建、维护和部署 Visual Studio 网络安装

有时，企业管理员希望创建包含可部署到客户端工作站的 Visual Studio 文件的网络安装点。 这是为了向以下情况提供辅助：客户端计算机具有的权限有限或对 Internet 的访问权限有限，或者组织希望对特定版本的开发人员工具集进行标准化。 我们设计了 Visual Studio，以便管理员可创建和维护网络布局（文件缓存），该网络布局可存储在内部网络共享上。 网络布局包含初始安装和后续产品更新所需的所有 Visual Studio 文件。

此网页中有很多信息，并已分组为以下部分：

- [**准备工作**](#before-you-get-started)：突出显示在规划时应考虑的提示和其他重要注意事项。
- [**获取正确的引导程序**](#download-the-visual-studio-bootstrapper-to-create-the-network-layout)：关于在何处查找以及如何区分可供你使用的各种引导程序的指南。
- [**创建网络布局**](#create-the-network-layout)：说明如何使用正确的产品内容、通道设置和安装程序版本创建布局，以及如何将其复制到网络共享。 
- [**更新、修改和维护网络布局**](#update-or-modify-your-layout)：关于如何以最佳方式维护布局的信息，包括如何更新布局的产品版本、产品内容、通道设置、安装程序版本和文件夹大小。 
- [**将布局安装到客户端计算机上**](#install-visual-studio-onto-a-client-machine-from-a-network-installation)：说明如何配置客户端默认设置，如默认情况下要安装的工作负载和组件，以及客户端应从何处查找更新。 此外，还包括如何在客户端计算机上执行 Visual Studio 布局的初始安装。 有关更新最初从布局安装的客户端计算机的指南和信息在单独的[更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)页面中有所介绍。
- [**帮助和支持**](#get-support-for-your-network-layout)：在何处寻求帮助

## <a name="before-you-get-started"></a>准备工作

在开始之前，有一些重要内容需要规划和注意。  
::: moniker range="vs-2017"

- **文件夹管理：** 如果企业使用多个 Visual Studio 版本（例如 Visual Studio 2017 Professional 和 Visual Studio 2017 Enterprise），则必须为每个版本单独创建网络安装点。 此外，原始 Visual Studio 安装布局和所有后续产品更新必须位于同一网络目录中，以确保客户端的修复和卸载功能正常工作。 最后，布局路径必须少于 80 个字符，尽管某些组织已成功使用[符号链接](/windows/win32/fileio/symbolic-links)来规避 80 个字符的限制。 
- **针对更新进行规划：** 必须在进行初始客户端安装前决定客户端计算机应以何种方式接收产品更新。 要确保正确设置客户端的更新位置配置，这一点必不可少。 你的选择包括让客户端从网络布局位置或 Internet 上的 Microsoft 托管服务器获取更新。 客户端从布局进行安装后，客户端的更新位置配置就会锁定，并无法更改。 

::: moniker-end

::: moniker range="vs-2019"

- **文件夹管理：** 如果企业使用多个 Visual Studio 版本（例如 Visual Studio 2019 Professional 和 Visual Studio 2019 Enterprise），则必须为每个版本单独创建网络安装点。 此外，布局路径必须少于 80 个字符，尽管某些组织已成功使用[符号链接](/windows/win32/fileio/symbolic-links)来规避 80 个字符的限制。 
- **针对更新进行规划：** 应该在进行初始客户端安装前决定客户端计算机应以何种方式接收产品更新。 要确保正确设置客户端的更新位置配置，这一点必不可少。 你的选择包括让客户端从网络布局位置或 Internet 上的 Microsoft 托管服务器获取更新。 

 > [!IMPORTANT]
 > 当你仅使用 Visual Studio 2019 功能时，布局管理存在以下限制：从布局安装客户端后，客户端的更新位置锁定且不可更改。 这意味着，如果你打算让客户端从布局接收更新，同时保留其修复和卸载功能，则必须将所有后续产品更新放在安装客户端的原始布局文件夹中。 换句话说，Visual Studio 2019 基本功能不支持客户端从一个布局位置执行原始安装，然后让该客户端从不同的布局位置接收产品更新。 
 > 
 > 产品更新位置固定且产品更新须位于与原始安装布局所在的同一布局文件夹中这种限制在 Visual Studio 2022 中不存在。 在 Visual Studio 2022 中，可以轻松更改客户端的源位置进行更新。 我们让你能够包括并使用最新的 (Visual Studio 2022) 安装程序（该安装程序可掌控 Visual Studio 产品系列的所有新式版本），以便管理 Visual Studio 2019 布局，并消除该产品 2019 版中的限制。 以下部分 [将布局配置为始终包含并提供最新的安装程序](#configure-the-layout-to-always-include-and-provide-the-latest-installer) ，介绍了如何启用此功能。
 
::: moniker-end

::: moniker range="vs-2022"

- **文件夹管理：** 如果企业使用多个 Visual Studio 版本（例如 Visual Studio 2022 Professional 和 Visual Studio 2022 Enterprise），则必须为每个版本单独创建网络安装点。 此外，布局路径必须少于 80 个字符，尽管某些组织已成功使用[符号链接](/windows/win32/fileio/symbolic-links)来规避 80 个字符的限制。
- **针对更新进行规划：** 建议在进行初始客户端安装前决定客户端计算机应以何种方式接收产品更新。 这是为了确保正确设置客户端的更新位置配置。 你的选择包括让客户端从网络布局位置或 Internet 上的 Microsoft 托管服务器获取更新。 幸运的是，还可以在执行初始安装后为更新配置客户端源位置。 

::: moniker-end

## <a name="download-the-visual-studio-bootstrapper-to-create-the-network-layout"></a>下载 Visual Studio 引导程序以创建网络布局

下载所需 Visual Studio 版本的引导程序，并将其复制到要用作布局源位置的目录中。 创建布局后，可将其用于将Visual Studio安装到任何客户端计算机上。 引导程序是用于创建、更新和执行其他布局操作的可执行文件。 必须连接 Internet 才能完成此步骤。

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 15.9 版的最新引导程序，请下载以下文件之一。 无论何时运行下面所列的引导程序，它们都将始终安装最新且最安全的 Visual Studio 2017 版本：

| 版本                                      | 引导程序            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Enterprise 版本 15.9   | [vs_enterprise.exe](https://aka.ms/vs/15/release/vs_enterprise.exe) |
| Visual Studio 2017 Professional 版本 15.9 | [vs_professional.exe](https://aka.ms/vs/15/release/vs_professional.exe) |
| Visual Studio 2017 生成工具版本 15.9  | [vs_buildtools.exe](https://aka.ms/vs/15/release/vs_buildtools.exe)   |

其他受支持的引导程序包括 vs_feedbackclient.exe、vs_teamexplorer.exe、vs_testagent.exe、vs_testcontroller.exe 和 vs_testprofessional.exe。

::: moniker-end

::: moniker range="vs-2019"

无论何时运行下面所列的引导程序，它们都将始终安装最新且最安全的 Visual Studio 2019 版本。 或者，如果要针对特定版本的 Visual Studio 2019 创建或更新布局，请转到 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)页（该页包含指向每个服务版本的固定版本引导程序的链接），然后下载所需版本。 将其复制到要用作布局源位置的目录中。

| 版本                                       | 引导程序                                                            |
|-----------------------------------------------|-------------------------------------------------------------------------|
| Visual Studio 2019 Enterprise 版本 16.11   | [vs_enterprise.exe](https://aka.ms/vs/16/release/vs_enterprise.exe)     |
| Visual Studio 2019 Professional 版本 16.11 | [vs_professional.exe](https://aka.ms/vs/16/release/vs_professional.exe) |
| Visual Studio 2019 生成工具版本 16.11  | [vs_buildtools.exe](https://aka.ms/vs/16/release/vs_buildtools.exe)     |

其他受支持的引导程序包括 [vs_teamexplorer.exe](https://aka.ms/vs/16/release/vs_TeamExplorer.exe)、[vs_testagent.exe](https://aka.ms/vs/16/release/vs_TestAgent.exe) 和 [vs_testcontroller.exe](https://aka.ms/vs/16/release/vs_TestController.exe)。

::: moniker-end

::: moniker range="=vs-2022"

无论何时运行下面所列的引导程序，它们都始终将在当前通道上安装最新且最安全的 Visual Studio 2022 版本。 或者，如果要针对 Visual Studio 2022 的特定版本或特定通道创建或更新布局，请转到 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页（该页包含指向各通道上每种服务版本的长期有效固定版本引导程序的链接），然后下载所需版本。 将其复制到要用作布局源位置的目录中。 

| 版本                    | 引导程序                                                        |
|----------------------------|----------------------------------------------------------------------|
| Visual Studio 2022 Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/release/vs_enterprise.exe)     |
| Visual Studio 2022 Professional | [vs_professional.exe](https://aka.ms/vs/17/release/vs_professional.exe) |
| Visual Studio 2022 生成工具   | [vs_buildtools.exe](https://aka.ms/vs/17/release/vs_buildtools.exe)         |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该版本号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 内部版本号和发布日期](visual-studio-build-numbers-and-release-dates.md)。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该编号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 2019 版本](/visualstudio/releases/2019/history)页面底部的表。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果你之前下载了一个引导程序文件，并且想要验证它将安装的版本，操作方法如下。 在 Windows 中，打开“文件资源管理器”，右键单击该引导程序文件，选择“属性”，然后选择“详细信息”选项卡。“产品版本”字段将描述该引导程序将安装的[频道和版本](/visualstudio/releases/2022/vs2022-release-rhythm)  。 版本号应始终读取为“指定内容的最新服务版本”，除非显式指定，否则假定通道为“当前”。 因此，产品版本为 LTSC 17.0 的引导程序将安装 17.0 LTSC 频道上提供的最新 17.0.x 服务版本。 产品版本仅显示“Visual Studio 2022”的引导程序将在当前频道上安装最新服务版本的 Visual Studio 2022。

::: moniker-end

## <a name="create-the-network-layout"></a>创建网络布局

必须具有 Internet 连接才能完成此步骤。

通过管理员特权打开命令提示符，导航到要下载引导程序的目标目录，并使用[使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md) 页中定义的引导程序参数来创建和维护网络布局。 下文和 [Visual Studio 安装的命令行参数示例](command-line-parameter-examples.md)页介绍了创建初始布局的常见示例。  

对于 Visual Studio Community，单一语言区域设置的完整初始布局需要约 35 GB 的磁盘空间，而 Visual Studio Enterprise 则需要约 45 GB 的磁盘空间。 其他每个[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)需要大约 0.5 GB 的磁盘空间。 
 
建议的方法是使用网络服务器上的布局目录中的所有语言和所有工作负载创建 Visual Studio Enterprise 的初始布局。 这样，客户端就有权访问整个产品/服务。 若要创建 Visual Studio 的完整布局，请从你计划用于托管网络布局的计算机上运行以下代码：

  ```vs_enterprise.exe --layout c:\VSLayout```
  
::: moniker range=">=vs-2022"

### <a name="ensure-your-layout-has-the-correct-channel"></a>确保布局具有正确通道

请务必确保网络布局基于正确[通道](/visualstudio/releases/2022/vs2022-release-rhythm)，因为这是[管理员更新](applying-administrator-updates.md)的条件之一，如果将其部署在整个组织中，请用于确定应更新的客户端实例。 例如，如果布局基于 VisualStudio.17.Release.LTSC.17.0 通道，并且客户端配置为从 Microsoft 托管服务器接收更新，则我们在 17.0 LTSC 通道上提供的任何安全更新都可供从该布局安装或更新的客户端使用。 

上面列出的引导程序基于当前通道。 若要基于其中一个 LTSC 通道创建布局，只需从 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页获取正确的通道引导程序，将其复制到布局文件夹中，然后使用它来创建或更新布局。 

::: moniker-end

### <a name="configure-the-contents-of-a-network-layout"></a>配置网络布局的内容

可使用多种选项自定义网络布局的内容。 可以创建仅包含一组特定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)、[工作负载、组件及其推荐或可选依赖项](workload-and-component-ids.md)的部分布局。 如果确定只会将部分工作负载部署到客户端工作站，部分布局就非常有用。 用于自定义布局的常见命令行参数包括：

* `--add`：用于指定[工作负载或组件 ID](workload-and-component-ids.md)。 <br>如果使用 `--add`，只会下载使用 `--add` 指定的工作负载和组件。  如果不使用 `--add`，将下载所有工作负载和组件。
* `--includeRecommended`，用于添加针对指定工作负载 ID 的所有推荐组件。
* `--includeOptional`，用于添加针对指定工作负载 ID 的所有可选组件。
* `--lang`：用于指定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)。

下面的几个示例展示了如何创建自定义部分布局。

* 若要仅针对一种语言创建具有所有工作负载和组件的布局，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* 若要针对多种语言创建具有所有工作负载和组件的布局，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* 若要针对所有语言创建包含一个工作负载以及该工作负载所有推荐组件的布局，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* 若要针对三种语言创建具有两个工作负载和一个可选组件的布局，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Microsoft.VisualStudio.Component.Git --lang en-US de-DE ja-JP
    ```

* 若要创建具有两个工作负载及其所有推荐和可选组件，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --includeRecommended --includeOptional
    ```
    
::: moniker range=">=vs-2019"

### <a name="ensure-your-layout-is-using-the-latest-installer"></a>确保布局使用最新安装程序

建议在布局中始终使用最新的 Visual Studio 安装程序并将其分发到客户端。 这样，你才能访问我们在产品后续版本中提供的新特性和功能。 例如，如果在 Visual Studio 2019 布局中分发 Visual Studio 2022 安装程序，则基于该布局的 Visual Studio 2019 客户端就能够更改更新的源位置。 对于从一种布局进行安装而让更新来自另一种布局的情况，此功能非常有用。 [下面介绍](#configure-the-layout-to-always-include-and-provide-the-latest-installer)了更多详细信息，包括如何使用最新安装程序进行关闭

 > [!IMPORTANT]
 > 使用最新安装程序这一功能适用于在 Visual Studio 2022 最初发布后生成的 Visual Studio 2019 引导程序。 因此，以下示例中的 vs_enterprise.exe 必须是 2021 年 11 月 10 日后发布的版本。 

* 若要使用最新和最好的可用安装程序创建整个产品的布局，请运行
    ```shell
    vs_enterprise.exe --layout C:\VSLayout --useLatestInstaller
    ```

::: moniker-end

### <a name="copy-the-layout-to-a-network-share"></a>将布局复制到网络共享

你需要将布局托管在网络共享上，以便户可以从其他客户端计算机运行。 如果在本地计算机上创建了布局，则需要将其复制到网络位置。 下面的示例使用 [`xcopy`](/windows-server/administration/windows-commands/xcopy/)。 如果愿意，也可使用 [`robocopy`](/windows-server/administration/windows-commands/robocopy/)。 示例：

```shell
xcopy /e c:\VSLayout \\server\share\layoutdirectory
```

> [!IMPORTANT]
> 为防止出现错误，请确保网络共享上的完整布局路径少于 80 个字符。 不过，某些组织已成功使用[符号链接](/windows/win32/fileio/symbolic-links)来规避 80 个字符的限制。

## <a name="update-or-modify-your-layout"></a>更新或修改布局

可以使用最新产品更新来更新 Visual Studio 的网络布局，以便可以将其用作客户端工作站的安装点和更新源，以接收最新版本的 Visual Studio。 最佳做法是定期更新布局，尤其是在希望客户端从布局接收更新的情况下。 本部分介绍最常见或有用的布局维护操作。

如果在 \\文件共享上托管布局，可能需要更新布局的专用副本 (例如 c：\VSLayout) ，然后在下载所有更新的内容后，将其复制到文件共享 (例如 \server\products\VS) 。 如果不这样做，那么在更新布局时正好运行安装程序的任何用户，都更有可能从布局中获得不匹配的内容，因为布局并未完全更新。

### <a name="update-the-layout-to-the-most-current-version-of-the-product"></a>将布局更新为产品的最新版本

Microsoft 经常发布产品的更新版本，以修复功能或安全问题。 我们建议使用最新版本的产品保持布局更新，以便新客户端安装始终收到最新的良好状态。 如果客户端配置为从布局接收更新，保持布局更新也很重要。 

创建初始布局时，指定的选项（例如要包括在布局中的工作负载和语言）保存在布局的配置文件中。 稍后，当你想要将布局更新为较新版本的产品时，就不必重新指定初始布局创建期间使用的选项。 布局更新命令会自动使用保存的布局设置。 

假设你已经使用[上表中的其中一款长期有效引导程序](#download-the-visual-studio-bootstrapper-to-create-the-network-layout)创建了这一部分布局。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

将此布局更新为 Microsoft 提供并托管在 Microsoft 服务器上的最新版产品非常简单。 只需使用相同的长期有效引导程序，然后再次运行 `--layout` 命令，将最新包下载到布局中。

```shell
vs_enterprise.exe --layout c:\VSLayout
```

还可以通过无人参与方式将布局更新为较新版本。 布局操作在新控制台窗口中运行设置进程。 该窗口保持打开状态，以便用户可以看到最终结果以及任何可能发生的错误的摘要。 如果以无人参与方式执行布局操作（例如，具有定期运行以将布局更新为最新版本的脚本），则使用 `--passive` 参数，进程会自动关闭窗口。

```shell
vs_enterprise.exe --layout c:\VSLayout --passive
```

### <a name="update-the-layout-to-a-specific-version-of-the-product"></a>将布局更新为产品的特定版本

有时，你可能要将布局更新为 _产品的特定版本_。  例如，你可能希望使布局与用于实现组织标准化的服务基线的最新安全版本相匹配。 下面是操作方法：

::: moniker range="vs-2019"

可以转到 [Visual Studio 2019 版本](/visualstudio/releases/2019/history#installing-an-earlier-release)页并下载特定的固定版本引导程序，将其复制到布局中，并使用它将布局更新到引导程序中指定的确切版本。 你将使用与上面完全相同的语法。

::: moniker-end

::: moniker range="vs-2022"

可以转到 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页并下载特定的固定版本引导程序，将其复制到布局中，并使用它将布局更新到引导程序中指定的确切版本。 你将使用与上面完全相同的语法。

::: moniker-end

可以使用[管理员更新](applying-administrator-updates.md)将布局更新到特定版本。 若要获取管理员更新，请转到 [Microsoft 更新目录](https://catalog.update.microsoft.com)，搜索要将布局更新到的更新。  将 update.exe 下载到托管布局的计算机，在该计算机上打开命令提示符并运行如下所示的命令：

```shell
visualstudioupdate-17.0.0to17.0.1.exe layout --layoutPath c:\VSLayout
```
请注意，管理员更新不会启动原始布局安装;它们仅会更新现有布局或客户端实例。 

::: moniker range=">=vs-2022"

### <a name="modify-the-channel-of-the-network-layout"></a>修改网络布局的通道

有时，当通道变得不受支持时，你需要确保网络布局继续基于受支持的通道，以便客户端可以继续接收安全更新通知。 如果布局基于 VisualStudio.17.Release.LTSC.17.0 通道，那么在 17.0 LTSC 通道不再受支持后，我们将不会对该通道发布任何其他安全更新程序，你的布局和客户端将变得不安全。

若要更改布局所基于的通道，只需从 [Visual Studio 2022 版本历史记录](/visualstudio/releases/2022/release-history#release-dates-and-build-numbers)页获取所需通道的引导程序，将其复制到布局文件夹中，并执行常规更新。 然后，应适当通知客户端更新，以便客户端也能够保持安全。

::: moniker-end

### <a name="modify-the-contents-of-the-layout"></a>修改布局的内容

可以修改此布局，并添加或删除其他工作负载、组件或语言。 在下面的示例中，我们将 Azure 工作负载和本地化语言添加到前面创建的布局中。 我们进行修改后，托管桌面和 Azure 工作负载以及英语和德语资源都将包含在此布局中。 此外，布局已更新至最新的可用版本。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

如果要修改现有部分布局，以便其成为完整布局，请使用 --all 选项，如以下示例所示。

```shell
vs_enterprise.exe --layout c:\VSLayout --all
```

有关如何在不更新版本的前提下添加其他工作负载和本地化语言的说明详见此处。 （此命令可添加 ASP.NET 和 Web 开发工作负载。）现在，托管桌面、Azure 以及 ASP.NET 和 Web 开发工作负载都已包含在此布局中。 这些工作负载中还加入了英语、德语和法语的语言资源。 但在运行此命令时，布局不会更新至最新的可用版本。 它将维持现有版本。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.NetWeb --lang fr-FR --keepLayoutVersion
```

 > [!IMPORTANT]
 > 更新操作不会将其他可选组件下载或安装到布局或客户端上。 如果需要添加或更改可选组件，请首先在 `layout.json` 配置文件中删除旧的可选组件，然后将所需的新组件添加到 `layout.json` 的“添加”部分。 然后，当你运行 `--layout` 命令以更新布局时，它会将新添加的组件下载到布局中。
 >
 > 若要在客户端计算机上安装这些新组件，请确保执行以下三个步骤。 首先，验证布局是否包含上述新组件。 接下来，在布局中将客户端更新为最新位。 最后，再次在客户端上运行修改操作，该操作会将新组件（已添加到布局中）安装到客户端计算机上。

::: moniker range=">=vs-2019"

### <a name="configure-the-layout-to-always-include-and-provide-the-latest-installer"></a>将布局配置为始终包含并提供最新的安装程序

可以将布局配置为 _始终_ 包含最新的安装程序，并为客户端提供最新安装程序，即使安装程序被视为最新版本的 Visual Studio。 因此，当客户端从此布局更新时，客户端将获取此布局包含和提供的最新安装程序。 好处是，在客户端上安装最新的安装程序后，客户端安装将能够利用 bug 修复和新功能，我们会继续将其添加到安装程序。 

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果要 [更改客户端 Visual Studio 2019 安装查找更新的位置](update-visual-studio.md#configure-source-location-of-updates)，则 *必须* 在客户端计算机上获取最新的 Visual Studio 2022 安装程序。 实现此目的的一种方法是使用下面所述的参数将 Visual Studio 2022 安装程序包含在 Visual Studio 2019 布局中。 使用最新安装程序的功能仅适用于最初发运 Visual Studio 2022 后构建 Visual Studio 2019 引导程序。 因此，以下示例中的 vs_enterprise.exe 必须是 2021 年 11 月 10 日后发布的版本。 

::: moniker-end

::: moniker range=">=vs-2019"

可以通过两种方式来包含和提供最新的安装程序：

- 创建或更新布局时，可以将 `--useLatestInstaller` 参数传递给引导程序。 这将导致在 layout.json 文件中进行一种设置，该文件位于布局的根目录中。 以下示例演示了如何更新布局以及如何将其配置为使用最新最好的可用安装程序。  


   ```shell
   vs_enterprise.exe --layout C:\VSLayout --useLatestInstaller
   ```

- 可以直接编辑 layout.json 文件以添加此设置。

   ```Example layout.json contents
   {
     "installChannelUri": ".\\ChannelManifest.json",
     "channelUri": "\\\\server\\share\\layoutdirectory\\ChannelManifest.json",
     "installCatalogUri": ".\\Catalog.json",
     "channelId": "VisualStudio.16.Release",
     "productId": "Microsoft.VisualStudio.Product.Enterprise",
   
     "useLatestInstaller": true
     
   }
   ```

无法以编程方式在 layout.json 文件中删除此设置，因此，如果希望布局停止使用 Microsoft 提供的最新安装程序，并改为使用与引导程序（很可能比最新安装程序版本旧）对应的安装程序版本，则只需编辑 layout.json 文件并删除 `"UseLatestInstaller": true` 设置即可。 

请注意，也可以在布局的响应. json 文件中找到此设置，但会忽略此 `"UseLatestInstaller": true` 设置。 [当客户端安装或从布局更新时，将使用响应 json 文件设置 _客户端_ 上的默认配置选项](automated-installation-with-response-file.md)。 此特定 `"useLatestInstaller": true` 设置用于确保 _布局_ 的内容包含最新的安装程序，以便客户端计算机可以从布局中获取最新的安装程序。

::: moniker-end

### <a name="verify-a-layout"></a>验证布局

使用 `--verify` 对网络布局执行验证，以检查包文件是否缺失或无效。 验证完成后，它将打印缺少和无效文件的列表。

验证仅适用于 Visual Studio 的特定次要版本的最新版本。 只要一发布新版本后，验证将不再适用于包含以前版本的布局。

```shell
vs_enterprise.exe --layout <layoutDir> --verify
```

> [!NOTE]
> `--verify` 选项所需的某些重要元数据文件必须位于布局文件夹内部。 如果缺少这些元数据文件，则无法运行“--verify”，且安装程序会出错。 如果遇到此错误，请尝试再次更新布局，或在另外的文件夹中重新创建一个新网络布局。

请记住，Microsoft 会定期向 Visual Studio 提供更新，因此较新的布局包含版本可能与初始布局不同，除非你使用[固定链接引导程序](#download-the-visual-studio-bootstrapper-to create-the-network-layout)。

### <a name="fix-a-layout"></a>修复布局

使用 `--fix` 执行与 `--verify` 相同的验证，并尝试修复标识的问题。 `--fix` 过程需要 Internet 连接，因此在调用 `--fix` 前请确保计算机已连接至 Internet。

```shell
vs_enterprise.exe --layout <layoutDir> --fix
```

### <a name="remove-older-versions-from-a-layout"></a>从布局中删除旧版本

对网络缓存执行布局更新后，布局文件夹中可能存在某些已过时的包，最新版本的 Visual Studio 安装不再需要这些包。 可使用 `--clean` 选项从网络布局文件夹中删除已过时的包。

要执行此操作，需要前往目录清单的文件路径，其中包含这些已过时的包。 可在网络布局缓存的“存档”文件夹中找到该目录清单。 更新布局时，这些目录清单就保存在此处。 在“存档”文件夹中，有一个或多个名为“GUID”的文件夹，其中每个都包含已过时的目录清单。 “GUID”文件夹数目应与布局的更新次数保持一致。

每个“GUID”文件夹中都保存着若干文件。 最重要的两个文件分别是“catalog.json”文件和“version.txt”文件。 “catalog.json”文件需要传递给 `--clean` 选项的已过时目录清单。 另一个 version.txt 文件则包含此已过时目录清单的版本。 根据版本号，可自行决定是否要从此目录清单中删除已过时包。 其他“GUID”文件夹中可执行同样的操作。 选择要清除的目录后，通过向这些目录提供文件路径来运行 `--clean` 命令。

下面是如何使用 --clean 选项的示例：

```shell
c:\VSLayout\vs_enterprise.exe --layout c:\VSLayout --clean c:\VSLayout\Archive\1cd70189-fc55-4583-8ad8-a2711e928325\Catalog.json --clean c:\VSLayout\Archive\d420889f-6aad-4ba4-99e4-ed7833795a10\Catalog.json
```

执行此命令时，安装程序会分析网络布局文件夹，以查找要删除的文件列表。 然后，可以对要删除的文件进行评审，并确认是否删除。

## <a name="install-visual-studio-onto-a-client-machine-from-a-network-installation"></a>通过网络安装将 Visual Studio 安装到客户端计算机上

管理员可以通过安装脚本将 Visual Studio 部署到客户端工作站上。 拥有管理员权限的用户也可以直接从共享运行安装程序，从而在自己的计算机上安装 Visual Studio。

* 用户可通过运行以下命令从网络布局手动安装产品：

    ```shell
    \\server\products\VS\vs_enterprise.exe
    ```

* 管理员可以通过运行以下命令在无人参与模式下进行安装：

    ```shell
    \\server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!NOTE] 
> 请耐心等待。 请确保 `--wait` 安装程序和产品都完成相关操作。 从布局安装或更新客户端时，安装程序始终最先安装或更新，然后再安装或更新 Visual Studio 产品本身。 这两个过程都要完成才能视为成功更新。   
>
> 无人参与的自动批处理文件这一过程中会执行安装或更新时，这时 `--wait` 选项有助于确保 `vs_enterprise.exe` 过程在返回退出代码之前等待安装完成。 如果企业管理员希望对已完成的安装执行其他操作（例如，[将产品密钥应用于成功的安装](automatically-apply-product-keys-when-deploying-visual-studio.md)），这就非常有用。 使用 --wait 选项可防止后续操作提前开始。 如果不使用 `--wait`，则 `vs_enterprise.exe` 进程可能会在安装的两个部分都完成之前退出，因此将返回不准确的退出代码，该代码不能表示安装操作状态。

### <a name="install-on-a-client-that-doesnt-have-internet-access"></a>在没有 Internet 访问的客户端上安装

通过布局安装时，安装内容将默认为从布局中获取。 但是，如果你选择的组件不在布局中，并且[客户端已配置为查看 Microsoft 托管服务器以获取更新](automated-installation-with-response-file.md)，则安装程序也会尝试从 Internet 获取 Visual Studio 包。 若要阻止 Visual Studio 安装程序尝试从 Web 下载布局中缺少的任何内容，请使用 `--noWeb` 选项。 如果使用 `--noWeb`，但布局中缺少要安装的选定内容，那么安装将会失败。

> [!IMPORTANT]
> 如果客户端已配置为查看 Microsoft 托管的服务器进行更新，则该 `--noWeb` 选项不会阻止连接 internet 的客户端计算机上的 Visual Studio 安装程序 _检查_ 更新。 相反， `--noWeb` 只会阻止客户端下载产品包。 有关详细信息，请参阅[更新从网络布局中安装的 Visual Studio 客户端](update-a-network-installation-of-visual-studio.md)。

::: moniker range=">=vs-2019"

如果收到一条错误消息，指出“找不到与以下参数匹配的项目”，请确保你使用了 `--noweb` 开关。

::: moniker-end

### <a name="configure-initial-client-installation-defaults-for-this-layout"></a>为此布局配置初始客户端安装默认值

可以修改布局文件夹中的一些文件，以设置最初在客户端计算机上安装产品时使用的默认值。 常见配置选项包括：

- 能够在初始安装期间 **配置应默认选择哪些工作负载、组件或语言**。 
- 能够指定 **客户端应从何处接收更新**。  选项来自管理员控制的网络布局位置，或者来自 Internet 上的 Microsoft 托管服务器（默认情况）。

有关如何为布局自定义和配置默认客户端设置的详细信息，请参阅[使用响应文件自动安装 Visual Studio](automated-installation-with-response-file.md)。  

### <a name="configure-enterprise-deployment-behavior"></a>配置企业部署行为

::: moniker range=">=vs-2019"

你还可以控制其他企业部署行为，如：

- 是否应启用管理员更新以及如何应用管理员更新。
- 可用更新通道有哪些，以及网络布局以何种方式在“更新设置”对话框中显示给客户端计算机。
- 共享包的安装位置。
- 是否要缓存及缓存位置。
- 通知的显示方式或者不显示通知。

有关其他详细信息，请参阅[为 Visual Studio 企业部署设置默认值](set-defaults-for-enterprise-deployments.md)。

::: moniker-end

::: moniker range="vs-2017"

还可以控制其他企业部署行为，例如安装共享包的位置。 有关其他详细信息，请参阅[为 Visual Studio 企业部署设置默认值](set-defaults-for-enterprise-deployments.md)。

::: moniker-end

### <a name="error-codes"></a>错误代码

如果使用 `--wait` 参数，`%ERRORLEVEL%` 环境变量会设置为下列值之一，具体视操作结果而定：

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

### <a name="get-support-for-your-network-layout"></a>获取对网络布局的支持

如果网络布局遇到问题，请告知我们。 通过[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具（会出现在 Visual Studio 安装程序和 Visual Studio IDE 中）是告知我们的最佳方式。 如果你是 IT 管理员，并且尚未安装 Visual Studio，可以[在此处提交 IT 管理员反馈](https://aka.ms/vs/admin/guide)。 使用此工具时，如果你可以发送 [VS 收集工具](https://aka.ms/vscollect)的日志，这将非常有帮助，可帮助我们诊断和解决问题。

对于安装相关问题，我们还提供[安装聊天](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项  。

我们还提供其他支持选项。 请参阅我们的 [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/home)。

## <a name="see-also"></a>请参阅

- [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
- [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
- [安装或使用 Visual Studio 时与网络相关错误的疑难解答](troubleshooting-network-related-errors-in-visual-studio.md)
- [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
- [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
- [在维修基线上更新 Visual Studio](update-servicing-baseline.md)
- [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
- [Visual Studio 工作负荷和组件 ID](workload-and-component-ids.md)
- [安装 Visual Studio 脱机安装所需的证书](install-certificates-for-visual-studio-offline.md)
