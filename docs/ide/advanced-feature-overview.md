---
title: 高级功能
description: 了解高级功能，这些功能可能更适合有经验的开发人员或已熟悉 Visual Studio 的开发人员。
ms.custom: vs-acquisition
ms.date: 10/01/2021
ms.topic: conceptual
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 136c66296e1980f3faae31dc0d5fc4c16fbaff57
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129431479"
---
# <a name="features-of-visual-studio"></a>Visual Studio 的功能

本文介绍的功能适合有经验的开发人员或已熟悉 Visual Studio 的开发人员。 有关 Visual Studio 的基本简介，请参阅 [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)。

## <a name="modular-installation"></a>模块化安装

在 Visual Studio 的模块化安装程序中，选择和安装所需的工作负载。 工作负载是编程语言或平台所需的功能组。 此模块化策略使安装 Visual Studio 占用的空间更小，因此安装和更新速度更快。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

要了解设置系统上的 Visual Studio 的详细信息，请参阅[安装 Visual Studio](../install/install-visual-studio.md)。

## <a name="create-cloud-enabled-azure-apps"></a>创建已启用云的 Azure 应用

Visual Studio 具有可用于轻松地创建已启用 Microsoft Azure 云的应用程序的工具套件。 可以从 Visual Studio 集成开发环境 (IDE) 直接配置、生成、调试、打包和部署 Azure 应用和服务。 若要获取 Azure 工具和项目模板，安装 Visual Studio 时请选择“Azure 开发”  工作负载。

::: moniker range="<=vs-2019"
![Visual Studio 安装程序中的 Azure 开发工作负载的屏幕截图。](../data-tools/media/azure-development-workload.png)
::: moniker-end
::: moniker range=">=vs-2022"
:::image type="content" source="media/vs-2022/azure-development-workload.png" alt-text="Visual Studio 安装程序中选择的 Azure 开发工作负载的屏幕截图。" border="false":::
::: moniker-end

::: moniker range="vs-2017"

安装“Azure 开发”工作负载后，“新建项目”对话框中将提供以下适用于 C# 的“云”模板    ：

![Visual Studio 云项目模板](media/cloud-project-templates.png)

::: moniker-end

::: moniker range="vs-2019"

在 Visual Studio 中，使用 [Cloud Explorer](/azure/vs-azure-tools-resources-managing-with-cloud-explorer) 来查看和管理基于 Azure 的云资源。 云资源可能包括虚拟机 (VM)、表和 SQL 数据库。 Cloud Explorer 可以显示登录的 Azure 订阅下的所有帐户中的 Azure 资源。 如果某一操作需要 Azure 门户，Cloud Explorer 会提供你在门户中所需位置的链接。

![Visual Studio 中“Cloud Explorer”的屏幕截图。](media/cloud-explorer.png)

::: moniker-end

::: moniker range=">=vs-2022"
> [!Important]
> “Cloud Explorer”窗口已在 Visual Studio 2022 中停用。 有关详细信息，请参阅[在 Visual Studio Cloud Explorer 中管理与 Azure 帐户关联的资源](../azure/vs-azure-tools-resources-managing-with-cloud-explorer.md?view=vs-2022&preserve-view=true)。
>
> 使用 Azure 门户根据需要访问 Azure 资源。 可以继续使用早期版本的 Visual Studio 中服务器资源管理器的 Azure 节点。
>
::: moniker-end

可通过添加以下连接服务为应用使用 Azure 服务：

- [Active Directory 连接服务](/azure/active-directory/develop/vs-active-directory-add-connected-service)，通过 [Azure Active Directory](/azure/active-directory/active-directory-whatis) (Azure AD) 帐户连接到 Web 应用
- [Azure 存储连接服务](/azure/vs-azure-tools-connected-services-storage)，该服务适用于 blob 存储、队列和表
- [密钥保管库连接服务](/azure/key-vault/vs-key-vault-add-connected-service)，可用于管理 Web 应用的机密

项目类型决定了可用的连接服务  。 右键单击“解决方案资源管理器”中的项目并选择“添加” > “连接服务”来添加服务。

::: moniker range="<=vs-2019"
![显示 Visual Studio 连接服务的屏幕截图。](media/connected-services.png)
::: moniker-end

::: moniker range=">=vs-2022"

在“连接服务”屏幕上，选择链接或加号以添加服务依赖关系。 在“添加依赖关系”屏幕上，选择要添加的服务，然后按照屏幕上的提示连接到 Azure 订阅和服务。

:::image type="content" source="media/vs-2022/connected-services.png" alt-text="显示连接服务依赖关系的屏幕截图。" border="false":::

::: moniker-end

有关详细信息，请参阅[使用 Visual Studio 和 Azure 移动到云](https://visualstudio.microsoft.com/vs/azure-tools/)。

## <a name="create-web-apps"></a>创建 Web 应用

Visual Studio 可以帮助你编写 Web 应用。 可以使用 ASP.NET、Node.js、Python、JavaScript 和 TypeScript 来创建 Web 应用。 Visual Studio 支持多种 Web 框架，如 Angular、jQuery 和 Express。

[ASP.NET Core](https://dotnet.microsoft.com/learn/aspnet/what-is-aspnet-core) 和 .NET Core 在 Windows、Mac 和 Linux 操作系统上运行。 ASP.NET Core 是 MVC、WebAPI 和 SignalR 的一个重大更新。 ASP.NET Core 旨在完全提供可组合的精益 .NET 堆栈，以便生成基于云的新式 Web 应用和服务。

有关详细信息，请参阅[新式 Web 工具](https://visualstudio.microsoft.com/vs/modern-web-tooling/)。

## <a name="build-cross-platform-apps-and-games"></a>生成跨平台应用和游戏

Visual Studio 可以生成适用于 macOS、Linux 和 Windows，以及 Android、iOS 和其他[移动设备](https://visualstudio.microsoft.com/vs/mobile-app-development/)的应用和游戏。 使用 Visual Studio 可以：

- 生成在 Windows、macOS 和 Linux 上运行的 [.NET Core](/dotnet/core/) 应用。

- 通过使用 [Xamarin](https://developer.xamarin.com/guides/cross-platform/windows/visual-studio/)，在 C# 和 F# 中生成适用于 iOS、Android 和 Windows 的移动应用。

- 通过使用 [Visual Studio Tools for Unity](/visualstudio/gamedev/unity/get-started/visual-studio-tools-for-unity)，在 C# 中生成 2D 和 3D 游戏。

- 生成适用于 iOS、Android 和 Windows 设备的本机 C++ 应用。 通过[适用于跨平台开发的 C++](/cpp/cross-platform/visual-cpp-for-cross-platform-mobile-development)，在 iOS、Android 和 Windows 库中分享通用代码。

## <a name="connect-to-databases"></a>连接到数据库

服务器资源管理器有助于你浏览和管理本地、远程以及 Azure、Microsoft 365、Salesforce.com 和网站上的服务器实例及资产。 若要打开“服务器资源管理器”，请选择“视图” > “服务器资源管理器”。 有关使用服务器资源管理器的详细信息，请参阅[添加新连接](../data-tools/add-new-connections.md)。

SQL Server 对象资源管理器提供类似于 SQL Server Management Studio 中的数据库对象。 使用 SQL Server 对象资源管理器可以执行轻负载数据库的管理和设计工作。 示例包括使用上下文菜单编辑表数据、对比架构和执行查询等等。

::: moniker range="<=vs-2019"
![显示“SQL Server 对象资源管理器”窗口的屏幕截图。](../ide/media/vs2015_sqlobjectexplorer.png)
::: moniker-end

::: moniker range=">=vs-2022"

若要打开“SQL Server 对象资源管理器”，请选择“服务器资源管理器”窗口顶部的图标，或从 Visual Studio 顶部菜单中选择“视图”>“SQL Server 对象资源管理器”。

:::image type="content" source="media/vs-2022/sql-server-object-explorer.png" alt-text="显示“SQL Server 对象资源管理器”窗口的屏幕截图。" border="false":::

::: moniker-end

[SQL Server Data Tools (SSDT)](/sql/ssdt/download-sql-server-data-tools-ssdt) 是一个适用于 SQL Server、Azure SQL 数据库和 Azure SQL 数据仓库的强大的开发环境。 通过 SSDT 可以生成、调试、维护和重构数据库。 可使用数据库项目，或直接使用已连接的数据库实例（本地或非本地）。 若要获取 SSDT，请使用 Visual Studio 安装程序安装“数据存储和处理”工作负载。

## <a name="debug-test-and-improve-your-code"></a>调试、测试和改进代码

编写代码时，应运行并测试该代码以了解 bug 和性能。 使用 Visual Studio 的调试系统，可以调试在本地项目、远程设备或[设备仿真器](../cross-platform/visual-studio-emulator-for-android.md)上运行的代码。 单步执行代码，一次执行一条语句，逐步检查变量。 或设置仅当指定条件为 true 时才命中的断点。 可以在代码编辑器中管理调试选项，因此无需离开代码。

有关 Visual Studio 中调试的详细信息，请参阅[调试器入门](../debugger/debugger-feature-tour.md)。

若要提高应用性能，请查看 Visual Studio [分析](../profiling/profiling-feature-tour.md)功能。

Visual Studio 提供单元测试、Live Unit Testing、IntelliTest、负载和性能测试等[测试](../test/improve-code-quality.md)选项。 Visual Studio 还拥有高级的[代码分析](../code-quality/code-analysis-for-managed-code-overview.md)功能，可查找设计、安全性和其他缺陷。

## <a name="deploy-your-finished-application"></a>部署完成的应用程序

Visual Studio 具有可用于通过 Microsoft Store、SharePoint 站点或者 InstallShield 或 Windows Installer 技术将应用部署到用户或客户的工具。 可以通过 Visual Studio IDE 访问所有这些选项。 有关详细信息，请参阅[部署应用程序、服务和组件](../deployment/deploying-applications-services-and-components.md)。

## <a name="manage-your-source-code-and-collaborate-with-others"></a>管理源代码并与他人协作

在 Visual Studio 中，可以在任意提供商（包括 GitHub）托管的 Git 存储库中管理源代码。 还可以通过浏览来查找要连接到的 Azure DevOps Server。

::: moniker range=">=vs-2022"

如需完整的详细信息，请参阅 [Visual Studio 中的 Git 体验](../version-control/git-with-visual-studio.md)页和 [Visual Studio 版本控制文档](../version-control/index.yml)导航页。 另外，有关如何使用 Visual Studio 连接到 Git 或 Azure DevOps 存储库的分步教程，请参阅[从存储库打开项目](../get-started/tutorial-open-project-from-repo.md?view=vs-2022&preserve-view=true)页。

> [!TIP]
> 我们会继续构建 Git 功能集，并根据你的反馈对它进行迭代。 若要获取有关最新功能更新的详细信息以及可在其中共享反馈的调查的链接，请参阅 [Visual Studio 中的多存储库支持](https://devblogs.microsoft.com/visualstudio/multi-repo-support-in-visual-studio/)博客文章。

::: moniker-end

::: moniker range="vs-2019"

使用 Visual Studio 2019 打开 GitHub 存储库中的项目的方式取决于你拥有的版本。 具体来说，如果你已安装 [16.8 版本](/visualstudio/releases/2019/release-notes/)或更高版本，则 Visual Studio 中提供了一个更完全集成的新 [Git 体验](../ide/git-with-visual-studio.md)供你使用。 有关详细信息，请参阅 [Visual Studio 版本控制文档](../version-control/index.yml)页。

另外，有关如何使用 Visual Studio 连接到 Git 或 Azure DevOps 存储库的分步教程，请参阅[从存储库打开项目](../get-started/tutorial-open-project-from-repo.md?view=vs-2019&preserve-view=true)页。

::: moniker-end

::: moniker range="vs-2017"

若要详细了解如何在 Visual Studio 中使用团队资源管理器管理 Git 存储库，请参阅[开始使用 Git 和 Azure Repos](/azure/devops/repos/git/gitquickstart?tabs=visual-studio)。 若要详细了解 Visual Studio 内置源代码管理功能，请参阅 [Visual Studio 中的 Git 功能](https://devblogs.microsoft.com/devops/new-git-features-in-visual-studio-2017/)博客文章。

[Azure DevOps Services](/azure/devops/index) 是一套基于云的服务，用于规划、托管、自动化和部署软件以及提升团队协作。 DevOps Services 支持 GitHub 分布式版本控制和 Team Foundation 版本控制 (TFVC) 集中式版本控制。 DevOps Services 为版本控制系统中存储的代码提供持续生成和发布 (CI/CD) 管道。 DevOps Services 还支持 Scrum、CMMI 和敏捷开发方法。 可以使用 DevOps Services 管理项目的代码、Bug 和工作项。

Team Foundation Server (TFS) 是 Visual Studio 的应用程序生命周期管理中心。 它使用单个解决方案，使开发过程中涉及的所有人均可参与该开发过程。 TFS 对于管理异类团队和项目也非常有用。

可以通过 Visual Studio“团队资源管理器”窗口在网络中连接到 Azure DevOps 组织或 Team Foundation Server。 可在“团队资源管理器”窗口中将代码签入（出）源控件、管理工作项、启动生成以及访问团队聊天室和工作区。 若要打开“团队资源管理器”，请使用搜索框，或选择“视图” > “团队资源管理器”。

下图展示了 Azure DevOps Services 中托管的解决方案的“团队资源管理器”窗口。

![连接到项目的 Visual Studio“团队资源管理器”窗口的屏幕截图。](../ide/media/vs2017_teamexplorer_devops.png)

Azure DevOps 是 Visual Studio 的应用程序生命周期管理中心。 Azure DevOps 使用单个解决方案，使开发过程中涉及的所有人均可参与该开发过程。 Azure DevOps 对于管理异类团队和项目也非常有用。

可以通过 Visual Studio 中的“团队资源管理器”窗口在网络中连接到 Azure DevOps 组织或 Azure DevOps Server。 可在“团队资源管理器”窗口中将代码签入（出）源控件、管理工作项、启动生成以及访问团队聊天室和工作区。 若要打开“团队资源管理器”，请使用搜索框，或选择“视图” > “团队资源管理器”。

你还可以自动执行生成过程，以生成开发人员签入到版本控制的代码。 例如，你可以在夜间或每次签入某个代码时生成一个或多个项目。 有关详细信息，请参阅 [Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true)。

::: moniker-end

## <a name="next-steps"></a>后续步骤

- 如果 Visual Studio 中没有你需要的确切功能，可以进行添加。 根据你的工作流和风格自定义 IDE，对尚未与 Visual Studio 集成的外部工具添加支持并修改现有的功能，以提高工作效率。 对于 Visual Studio 扩展性工具 (VS SDK) 的最新版本，请参阅 [Visual Studio SDK](../extensibility/visual-studio-sdk.md)。

- 可使用 .NET Compiler Platform（“Roslyn”）自行编写代码分析器和代码生成器。 在 [Roslyn](https://github.com/dotnet/Roslyn)中查找所需的一切内容。

- 查找由 Microsoft 开发人员以及 Visual Studio 开发社区创建的 Visual Studio [现有扩展](https://marketplace.visualstudio.com/vs)。

- 若要了解有关扩展 Visual Studio 的详细信息，请参阅[扩展 Visual Studio IDE](https://visualstudio.microsoft.com/vs/extend/)。

## <a name="see-also"></a>另请参阅

- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
- [Visual Studio 2017 中的新增功能](../ide/whats-new-visual-studio-2017.md)
- [Visual Studio 2019 中的新增功能](../ide/whats-new-visual-studio-2019.md)
- [Visual Studio 2022 中的新增功能](whats-new-visual-studio-2022.md)