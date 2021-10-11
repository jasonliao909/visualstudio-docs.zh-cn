---
title: 创建基于网络的安装
description: 了解如何创建用于在企业中部署 Visual Studio 的网络安装点。
ms.date: 04/06/2021
ms.custom: seodec18
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
ms.openlocfilehash: 978a6676acc32336646140ee38e75d499697a457
ms.sourcegitcommit: aaa3146356421d921714c29ffd586083570ade3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2021
ms.locfileid: "129635602"
---
# <a name="create-a-network-installation-of-visual-studio"></a>创建 Visual Studio 的网络安装

有时，企业管理员希望创建包含可部署到客户端工作站的 Visual Studio 文件的网络安装点。 这是为了帮助解决客户端计算机具有有限的权限或对 Internet 的访问权限有限的情况，或者当内部团队想要在其组织对特定版本的开发人员工具集进行标准化之前进行兼容性测试时的情况。 我们设计了 Visual Studio 以便管理员可以创建一个网络布局，该网络布局实质上是创建一个位于内部静态网络共享上的文件缓存，其中包括用于初始安装和未来所有产品更新的所有 Visual Studio 文件。

 > [!NOTE]
 >  - 如果企业使用多个 Visual Studio 版本（例如，同时使用 Visual Studio 2019 Professional 和 Visual Studio 2019 Enterprise），则必须为每个版本单独创建网络安装共享。
 >  - 建议你在执行初始客户端安装之前确定你希望客户端如何接收产品更新。  这样可以更轻松地确保正确设置配置选项。 你的选择包括让客户端从网络布局位置或从 Internet 获取更新。 
 >  - 原始 Visual Studio 安装布局和所有后续产品更新必须位于同一网络目录中，以确保修复和卸载功能正常工作。

## <a name="download-the-visual-studio-bootstrapper"></a>下载 Visual Studio 引导程序

下载适用于所需版本的 Visual Studio 的引导程序文件。 请确保选择“保存”，然后选择“打开文件夹”   。

::: moniker range="vs-2017"

若要获取 Visual Studio 2017 版本15.9 的最新引导程序，请转到 [Visual Studio 以前的版本](https://visualstudio.microsoft.com/vs/older-downloads/)页，并下载以下引导程序文件之一：

| 版本                                      | Filename            |
|----------------------------------------------|---------------------|
| Visual Studio 2017 Enterprise 版本 15.9   | vs_enterprise.exe   |
| Visual Studio 2017 Professional 版本 15.9 | vs_professional.exe |
| Visual Studio 2017 生成工具版本 15.9  | vs_buildtools.exe   |

其他受支持的引导程序包括 vs_feedbackclient.exe、vs_teamexplorer.exe、vs_testagent.exe、vs_testcontroller.exe 和 vs_testprofessional.exe。

::: moniker-end

::: moniker range="vs-2019"

首先从 [Visual Studio 下载页](https://visualstudio.microsoft.com/downloads)或 [Visual Studio 2019 版](/visualstudio/releases/2019/history#installing-an-earlier-release)页下载 Visual Studio 2019 引导程序，以找到所选版本的 Visual Studio。  安装程序可执行文件（更具体而言，是引导程序文件）应与以下其中一项匹配，或与之类似：

| 版本                    | 下载                                                                                                                                                                                                                           |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=enterprise&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019)     |
| Visual Studio Professional | [vs_professional.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=professional&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=network+install&utm_content=download+vs2019) |
| Visual Studio 生成工具  | [vs_buildtools.exe](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=buildtools&rel=16&utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=offline+install&utm_content=download+vs2019)     |

其他受支持的引导程序包括 [vs_teamexplorer.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/4026077127d25d33789f3882998266946608d8ada378b6ed7c8fff8c07f3dde2/vs_TeamExplorer.exe)、[vs_testagent.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/1383bf8bcda3d0e986a2e42c14114aaea8a7b085d31aa0623c9f70b2bad130e4/vs_TestAgent.exe) 和 [vs_testcontroller.exe](https://download.visualstudio.microsoft.com/download/pr/f6473c9f-a5f6-4249-af28-c2fd14b6a0fb/54dcf24b76e7cd9fb8be0ac518a9dfba6daf18fe9b2aa1543411b1cda8820918/vs_TestController.exe)。

::: moniker-end

::: moniker range=">=vs-2022"

>![!TIP]
> 发布的 Visual Studio 2022 版尚不可用，以下引导程序适用于 Visual Studio 2022 预览版。
首先从 [Visual Studio 下载页](https://aka.ms/vs2022preview)下载 Visual Studio 2022 引导程序。

| 版本                    | 下载                                                                             |
|----------------------------|--------------------------------------------------------------------------------------|
| Visual Studio Enterprise   | [vs_enterprise.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_enterprise.exe)     |
| Visual Studio Professional | [vs_professional.exe](https://aka.ms/vs/17/preview/bootstrapper/vs_professional.exe) |

::: moniker-end

::: moniker range="vs-2017"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该版本号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 内部版本号和发布日期](visual-studio-build-numbers-and-release-dates.md)。

::: moniker-end

::: moniker range="vs-2019"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该版本号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 2019 版](/visualstudio/releases/2019/history)。

::: moniker-end

::: moniker range=">=vs-2022"

>[!TIP]
>如果以前下载过引导程序文件，并且想要验证其版本，操作方法如下。 在 Windows 中，打开文件资源管理器，右键单击引导程序文件，依次选择“属性”、“详细信息”选项卡，然后查看“产品版本”号    。 若要将该版本号与 Visual Studio 的版本匹配，请参阅 [Visual Studio 2022 版](/visualstudio/releases/2022/history)。

::: moniker-end

## <a name="create-an-offline-installation-folder"></a>创建脱机安装文件夹

必须具有 Internet 连接才能完成此步骤。

打开命令提示符，导航到要下载引导程序的目标目录，并使用[使用命令行参数安装 Visual Studio](../install/use-command-line-parameters-to-install-visual-studio.md) 页中定义的引导程序参数来创建和维护网络安装缓存。 下文和 [Visual Studio 安装的命令行参数示例](../install/command-line-parameter-examples.md)介绍了创建初始布局的常见示例。  

   > [!IMPORTANT]
   > 对于 Visual Studio Community，单一语言区域设置的完整初始布局需要约 35 GB 的磁盘空间，而 Visual Studio Enterprise 则需要约 42 GB 的磁盘空间。 其他每个[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)需要大约 0.5 GB 的磁盘空间。 有关详细信息，请参阅[自定义网络布局](#customize-the-network-layout)部分。 请注意，后续布局更新也必须存储在同一网络位置，因此，网络布局位置的目录内容可能会随着时间的推移而变得非常大。  

- 若要创建具有所有语言和所有功能的 Visual Studio Enterprise 的初始布局，请运行：

  ```vs_enterprise.exe --layout c:\VSLayout```

- 若要创建具有所有语言和所有功能的 Visual Studio Professional 的初始布局，请运行：

  ```vs_professional.exe --layout c:\VSLayout```

## <a name="modify-the-responsejson-file"></a>修改 response.json 文件

可以通过修改 `response.json` 来设置用户在运行安装程序时使用的默认值。  例如，可以通过配置 `response.json` 文件来选择一组应自动选定的特定工作负荷。 你还可以将配置 `response.json`，以指定客户端是否应仅从网络布局位置接收更新的文件。 有关详细信息，请参阅[通过响应文件自动执行 Visual Studio 安装](../install/automated-installation-with-response-file.md)。 

如果在将引发错误的 Visual Studio 引导程序与 `response.json` 文件配对时发生错误，请参阅[安装或使用 Visual Studio 时与网络相关错误的疑难解答](../install/troubleshooting-network-related-errors-in-visual-studio.md#error-failed-to-parse-id-from-parent-process)页，以获取详细信息。

## <a name="copy-the-layout-to-a-network-share"></a>将布局复制到网络共享

将布局托管在网络共享上，以便用户可以从其他客户端计算机运行。

下面的示例使用 [`xcopy`](/windows-server/administration/windows-commands/xcopy/)。 如果愿意，也可使用 [`robocopy`](/windows-server/administration/windows-commands/robocopy/)。

::: moniker range="vs-2017"

示例：

```shell
xcopy /e c:\VSLayout \\server\products\VS2017
```

::: moniker-end

::: moniker range="vs-2019"

```shell
xcopy /e c:\VSLayout \\server\products\VS2019
```

::: moniker-end

::: moniker range=">=vs-2022"

```shell
xcopy /e c:\VSLayout \\server\products\VS2022
```

::: moniker-end

> [!IMPORTANT]
> 为了防止错误出现，请确保完整布局路径的长度小于 80 个字符。

## <a name="customize-the-network-layout"></a>自定义网络布局

可使用多个选项自定义网络布局。 可以创建仅包含一组特定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)、[工作负载、组件及其推荐或可选依赖项](workload-and-component-ids.md)的部分布局。 如果确定只会将部分工作负载部署到客户端工作站，部分布局就非常有用。 用于自定义布局的常见命令行参数包括：

* `--add`：用于指定[工作负载或组件 ID](workload-and-component-ids.md)。 <br>如果使用 `--add`，只会下载使用 `--add` 指定的工作负载和组件。  如果不使用 `--add`，将下载所有工作负载和组件。
* `--includeRecommended`：用于添加针对指定工作负载 ID 的所有推荐组件
* `--includeOptional`：用于添加针对指定工作负载 ID 的所有推荐和可选组件。
* `--lang`：用于指定[语言区域设置](use-command-line-parameters-to-install-visual-studio.md#list-of-language-locales)。

下面的几个示例展示了如何创建自定义部分布局。

* 若要下载仅一种语言的所有工作负载和组件，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US
    ```

* 若要下载多种语言的所有工作负载和组件，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --lang en-US de-DE ja-JP
    ```

* 若要下载所有语言的一个工作负载，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --includeRecommended
    ```

* 若要下载三种语言的两个工作负载和一个可选组件，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended --lang en-US de-DE ja-JP
    ```

* 下载两个工作负载及其所有推荐组件：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeRecommended
    ```

* 若要下载两个工作负载及其所有推荐和可选组件，请运行：

    ```shell
    vs_enterprise.exe --layout C:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --add Microsoft.VisualStudio.Workload.ManagedDesktop --add Component.GitHub.VisualStudio --includeOptional
    ```

### <a name="save-your-layout-options"></a>保存布局选项

运行布局命令时，指定的选项（例如工作负载和语言）将被保存。 后续的布局命令将包括先前的所有选项。  以下示例说明如何使用一个工作负载来创建布局（仅限英语）：

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.ManagedDesktop --lang en-US
```

若要将布局更新至较新版本，无需指定任何额外命令行参数。 此布局文件夹中的任何后续布局命令都将使用先前所保存的设置。  以下命令将更新现有的部分布局。

```shell
vs_enterprise.exe --layout c:\VSLayout
```

有关添加其他工作负载的相关操作说明，请参阅下列示例。 在此事例中，我们将添加 Azure 工作负载和已本地化的语言。  现在，此布局中已包括托管桌面和 Azure。  所有这些工作负载中都加入了英语和德语的语言资源。 已将布局更新至最新的可用版本。

```shell
vs_enterprise.exe --layout c:\VSLayout --add Microsoft.VisualStudio.Workload.Azure --lang de-DE
```

要将现有布局更新至完整布局，请使用 --all 选项，如下方示例所示。

```shell
vs_enterprise.exe --layout c:\VSLayout --all
```

## <a name="deploy-from-a-network-installation"></a>从网络安装点进行部署

管理员可以通过安装脚本将 Visual Studio 部署到客户端工作站上。 拥有管理员权限的用户也可以直接从共享运行安装程序，从而在自己的计算机上安装 Visual Studio。

* 用户可通过运行以下命令进行安装： <br>

    ```shell
    \\server\products\VS\vs_enterprise.exe
    ```

* 管理员可以通过运行以下命令在无人参与模式下进行安装：

    ```shell
    \\server\products\VS\vs_enterprise.exe --quiet --wait --norestart
    ```

> [!IMPORTANT]
> 为了防止错误出现，请确保完整布局路径的长度小于 80 个字符。

> [!TIP]
> 如果作为批处理文件的一部分执行，`--wait` 选项可确保 `vs_enterprise.exe` 进程先等待安装完成，再返回退出代码。
>
> 若企业管理员要在已完成的安装上执行进一步操作（例如，[向已成功的安装应用产品密钥](automatically-apply-product-keys-when-deploying-visual-studio.md)），此方法十分有用，但需要等待安装完成以处理从该安装返回的代码。
>
> 如果不使用 `--wait``vs_enterprise.exe` 进程将在安装完成前退出，并返回一个不能表示安装操作状态的不准确的退出代码。
>

::: moniker range=">=vs-2019"
> [!IMPORTANT]
> 对于脱机安装，如果收到一条错误消息，指出“找不到与以下参数匹配的项目”，请确保将 `--noweb` 开关用于版本 16.3.5 或更高版本。
>
::: moniker-end

从布局安装时，安装内容将从布局中获取。 但是，如果选择不在布局中的组件，则会从 Internet 获取它。  要阻止 Visual Studio 安装程序下载布局中缺少的任何内容，请使用 `--noWeb` 选项。 如果使用 `--noWeb`，但布局中缺少要安装的选定内容，安装就会失败。

> [!TIP]
> 如果要从未连接 Internet 的计算机上的脱机源进行安装，请指定 `--noWeb` 和 `--noUpdateInstaller` 选项。 前者科阻止下载更新的工作负载、组件等。 后者可阻止安装程序通过 Web 进行自我更新。

> [!IMPORTANT]
> `--noWeb` 选项不会阻止已连接 Internet 的计算机上的 Visual Studio 安装程序检查更新。 有关详细信息，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)页。

### <a name="error-codes"></a>错误代码

如果使用 `--wait` 参数，`%ERRORLEVEL%` 环境变量会设置为下列值之一，具体视操作结果而定：

[!INCLUDE[install-error-codes-md](includes/install-error-codes-md.md)]

## <a name="update-a-network-install-layout"></a>更新网络安装布局

有产品更新时，可能需要[更新网络安装布局](update-a-network-installation-of-visual-studio.md)以纳入更新后的包。

## <a name="how-to-create-a-layout-for-a-previous-visual-studio-release"></a>如何为旧版 Visual Studio 创建布局

首先，你需要了解有两种类型的 Visual Studio 引导程序，一种可以具有“最新”、“当前”、“长期有效”和“提示”等特征，另一个本质上表示“固定版本”。 这两种类型的引导程序文件具有完全相同的名称，因此，区分类型的最佳方式是关注其来源。 Visual Studio 引导程序可从 [Visual Studio 下载页面](https://visualstudio.microsoft.com/downloads)获得，并被视为长期有效 Visual Studio 引导程序，且它们始终会安装（或更新）在引导程序运行时通道中可用的最新版本。 [Visual Studio 2019 版](/visualstudio/releases/2019/history)和 [Visual Studio 2022 版](/visualstudio/releases/2022/history)页面上提供的 Visual Studio 引导程序，或嵌入在 Microsoft 更新目录中的管理员更新中的 Visual Studio 引导程序将安装该产品的特定固定版本。

因此，如果立即下载长期有效的 Visual Studio 引导程序，并从现在开始运行 6 个月，则会安装运行引导程序时的最新 Visual Studio 版本。 它旨在始终安装最新的位并使你保持最新。

如果下载了固定链接的引导程序，或者运行从 Microsoft 目录下载的管理员更新，则它将始终安装特定版本的产品，而不考虑其运行时间。

最后，你可以使用这些引导程序中的任何一个创建网络布局，将在布局中创建的版本取决于你使用的引导程序，例如，版本可以是固定版本或当前版本。 然后，你可以使用任何更高版本的引导程序更新网络布局，也可以使用 Microsoft 更新目录中的管理员更新包。 无论更新布局的方式如何，生成的更新布局都将是包含产品特定版本的包缓存，随后其行为将类似于固定链接引导程序。 因此，每当从布局中安装客户端时，客户端都将安装布局中存在的特定版本的 Visual Studio（即使线上存在较高版本也是如此）。

### <a name="how-to-get-support-for-your-offline-installer"></a>如何获取关于脱机安装程序的支持

如果脱机安装遇到问题，请告知我们。 告知我们的最好方式是使用[报告问题](../ide/how-to-report-a-problem-with-visual-studio.md)工具。 使用此工具时，可发送我们诊断和修复问题所需的遥测数据和日志。

对于安装相关问题，我们还提供[安装聊天](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项  。

我们还提供其他支持选项。 请参阅[开发人员社区](https://developercommunity.visualstudio.com/home)。

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
