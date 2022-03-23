---
title: 初探部署
description: 了解从 Visual Studio 部署应用的选项。
ms.date: 10/29/2021
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- .NET applications, deploying
- components [Visual Studio], deploying
- installers
- publishing
- deploying applications [Visual Studio]
- deploying applications [Visual Studio], about deploying applications
- components [.NET Framework], deploying
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: a9e9811763c04fe2b469162843a4f241cffad59f
ms.sourcegitcommit: 00af065ac27d41339b31d96a630705509b70b6fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2022
ms.locfileid: "140764422"
---
# <a name="first-look-at-deployment-in-visual-studio"></a>先查看 Visual Studio 中的部署

通过部署应用程序、服务或组件，你可以将其分发以便安装于其他计算机、设备、或服务器上，或云中。 你需要在 Visual Studio 中为所需的部署类型选择适当的方法。 （许多应用类型支持此处未描述的其他部署工具，如命令行部署或 NuGet。）

有关分步部署说明，请参阅快速入门和教程。 有关部署选项的概述，请参阅[哪些发布选项适合我？](deploying-applications-services-and-components-resources.md#what-publishing-options-are-right-for-me)

## <a name="deploy-to-a-local-folder"></a>部署到本地文件夹

部署到本地文件夹通常用于测试，或开始分阶段部署，其中使用另一个工具进行最终部署。

- **ASP.NET**、**ASP.NET Core**、**Node.js**、**Python** 和 .**NET Core**：使用发布工具部署到本地文件夹。 可用的具体选项取决于应用类型。 在解决方案资源管理器中，右键单击项目，并选择“发布”。 （如果之前尚未配置任何发布配置文件，必须选择“新建配置文件”。）接下来选择“文件夹”。 有关详细信息，请参阅[发布 ASP.NET 应用](quickstart-deploy-aspnet-web-app.md?tabs=folder)。

    ![显示选择“发布”的屏幕截图。](../deployment/media/quickstart-publish.png)

- **Windows 桌面**：可以使用 ClickOnce 部署将 Windows 桌面应用程序发布到文件夹。 用户随后只需一次单击即可安装应用程序。 有关详细信息，请参阅以下文章：

  - [使用 ClickOnce 部署 .NET Windows 桌面应用](quickstart-deploy-using-clickonce-folder.md)
  - [使用 ClickOnce 部署 .NET Framework Windows 桌面应用。](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
  - 请参阅[使用 ClickOnce 部署 C++/CLR 应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)，对于 C/C++，请参阅[使用安装项目部署本机应用](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)。

## <a name="publish-to-azure"></a>发布到 Azure

- **ASP.NET**、**ASP.NET Core**、**Python** 和 **Node.js**：使用以下任一方法发布到 Azure 应用服务或 Linux 上的 Azure 应用服务（使用容器）：

  - 对于应用的连续（或自动）部署，请将 Azure DevOps 与 Azure 管道结合使用。
  - 对于应用的一次性（或手动）部署，请使用 Visual Studio 中的“发布”工具。
  - 若要为 GitHub.com 上托管的 ASP.NET 和 Azure Function 项目创建 GitHub 操作工作流，请参阅[使用 GitHub Actions 部署到 Azure](../deployment/azure-deployment-using-github-actions.md)。

  对于可提供自定义程度更高的服务器配置的部署，还可以使用“发布”工具将应用部署到 Azure 虚拟机。

  要使用“发布”工具，请右键单击“解决方案资源管理器”中的项目，然后选择“发布”。 （如果之前尚未配置任何发布配置文件，必须选择“新建配置文件”。）在“发布”对话框中，选择“应用服务”或“Azure 虚拟机”，然后按照配置步骤操作。

  ![显示选择“Azure 应用服务”的屏幕截图。](../deployment/media/quickstart-publish-azure-new.png "选择 Azure 应用服务")

  自 Visual Studio 2017 版本 15.7 开始，可将 ASP.NET Core 应用部署到 Linux 上的应用服务。

  有关快速介绍，请参阅[发布 ASP.NET 应用](quickstart-deploy-aspnet-web-app.md?tabs=folder)。 另请参阅[部署 ASP.NET Web 应用](/azure/app-service/quickstart-dotnetcore?tabs=netcore31&pivots=development-environment-vs#publish-your-web-app)。 有关使用 Git 进行部署的信息，请参阅[使用 Git 将 ASP.NET Core 持续部署到 Azure](/azure/app-service/deploy-continuous-deployment)。

  > [!NOTE]
  > 如果没有 Azure 帐户，可以[在此注册](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=doc&utm_campaign=visualstudio)。

## <a name="publish-to-the-web-or-deploy-to-a-network-share"></a>发布到 Web 或部署到网络共享

- **ASP.NET**、**ASP.NET Core**、**Node.js** 和 **Python**：可以通过 FTP 或 Web 部署使用发布工具部署到网站。 有关详细信息，请参阅[发布 ASP.NET 应用](quickstart-deploy-aspnet-web-app.md?tabs=folder.md?tabs=web-server)。

    在“解决方案资源管理器”中，右键单击项目，然后选择“发布”。 （如果之前尚未配置任何发布配置文件，必须选择“新建配置文件”。）在发布工具中，选择想要的选项并遵循配置步骤。

    ![显示选择“IIS”的屏幕截图。](../deployment/media/quickstart-publish-iis.png)

    有关在 Visual Studio 中导入发布配置文件的信息，请参阅[导入发布设置并部署到 IIS](../deployment/tutorial-import-publish-settings-iis.md)。

    也可以采用多种不同的方式部署 ASP.NET 应用程序和服务。 有关详细信息，请参阅[部署 ASP.NET Web 应用程序和服务](/aspnet/web-forms/overview/deployment/visual-studio-web-deployment/)。

- **Windows 桌面**：可以使用 ClickOnce 部署将 Windows 桌面应用程序发布到 Web 服务器或网络文件共享。 用户随后只需一次单击即可安装应用程序。 有关详细信息，请参阅以下文章：

  - [使用 ClickOnce 部署 .NET Framework Windows 桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
  - [使用 ClickOnce 部署 .NET Windows 桌面应用](quickstart-deploy-using-clickonce-folder.md)
  - [使用 ClickOnce 部署 C++/CLR 应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)

## <a name="create-an-installer-package-windows-desktop"></a>创建安装程序包（Windows 桌面）

如果需要比 ClickOnce 提供的更为复杂的桌面应用程序安装，则可以创建 Windows Installer 包（MSI 或 EXE 安装文件）或自定义引导程序。

- 可以使用 [WiX 工具集 Visual Studio 2017 扩展](https://marketplace.visualstudio.com/items?itemName=RobMensching.WixToolsetVisualStudio2017Extension)创建基于 MSI 的安装程序包。 这是一个命令行工具集。

- 可以使用安装项目 (vdproj) 创建 MSI 或 EXE 安装程序包。 若要使用此选项，请参阅 [Visual Studio 安装程序扩展和 .NET Core 3.1 和 .NET 5.0](../deployment/installer-projects-net-core.md)，或者直接转到 [Visual Studio 安装程序项目扩展](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.MicrosoftVisualStudio2017InstallerProjects#overview)。

- 可以使用 Flexera Software 中的 [InstallShield](https://www.flexerasoftware.com/producer/products/software-installation/installshield-software-installer/tab/requirements) 创建 MSI 或 EXE 安装程序包。 InstallShield 可与 Visual Studio 2017 及更高版本一起使用。 不支持 Community Edition。

  > [!NOTE]
  > InstallShield Limited Edition 不再包含在 Visual Studio 中，且不受 Visual Studio 2017 及更高版本支持。 请查看 [Flexera Software](http://learn.flexerasoftware.com/content/IS-EVAL-InstallShield-Limited-Edition-Visual-Studio)，了解其未来的可用性。

- 还可以通过配置通用安装程序（称为引导程序）来安装桌面应用程序的必备组件。 有关详细信息，请参阅[应用程序部署必备](../deployment/application-deployment-prerequisites.md)。

## <a name="publish-to-microsoft-store"></a>发布到 Microsoft Store

可以从 Visual Studio 中创建用于部署到 Microsoft Store 的应用程序包。

- **UWP**：可以使用菜单项将应用打包并部署。 有关详细信息，请参阅[使用 Visual Studio 打包 UWP 应用](/windows/uwp/packaging/packaging-uwp-apps)。

    ![显示创建应用包的屏幕截图。](../deployment/media/feature-tour-create-app-package.png)

- **Windows 桌面**：从 Visual Studio 2017 15.4 版开始可以使用桌面桥部署到 Microsoft Store。 若要执行此操作，首先创建一个 Windows 应用程序打包项目。 有关详细信息，请参阅[为 Microsoft Store 打包桌面应用（桌面桥）](/windows/uwp/porting/desktop-to-uwp-packaging-dot-net)。

    ![显示选择“Windows 应用程序打包项目”的屏幕截图。](../deployment/media/feature-tour-desktop-bridge.png)

## <a name="deploy-to-a-device-uwp"></a>部署到设备 (UWP)

如果要将用于测试 的 UWP 应用部署到设备，请参阅[在 Visual Studio 中在远程计算机上运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)。

## <a name="deploy-to-a-test-lab"></a>部署到测试实验室

可以通过将应用程序部署到虚拟环境中来实现更复杂的开发和测试。 有关详细信息，请参阅[在实验室环境测试](../test/lab-management/using-a-lab-environment-for-your-application-lifecycle.md)。

## <a name="continuous-deployment"></a>连续部署

可以使用 Azure Pipelines 以实现应用的连续部署。 有关详细信息，请参阅 [Azure Pipelines](/azure/devops/pipelines/index?view=vsts&preserve-view=true) 和[部署到 Azure](/azure/devops/pipelines/overview-azure)。

## <a name="deploy-a-sql-database"></a>部署 SQL 数据库

- [更改目标平台并发布数据库项目 (SQL Server Data Tools (SSDT))](/sql/ssdt/how-to-change-target-platform-and-publish-a-database-project)
- [部署 Analysis Services 项目 (SSAS)](/sql/analysis-services/multidimensional-tutorial/lesson-2-5-deploying-an-analysis-services-project)
- [部署 Integration Services (SSIS) 项目和包](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages)
- [生成并部署到本地数据库](/sql/ssdt/how-to-build-and-deploy-to-a-local-database)

## <a name="deployment-for-other-app-types"></a>其他应用类型的部署

| 应用类型 | 部署场景 | 链接 |
| --- | --- | --- |
| **Office 应用** | 可以从 Visual Studio 发布 Office 的加载项。 | [部署和发布 Office 加载项](/office/dev/add-ins/publish/publish) |
| **WCF 或 OData 服务** | 其他应用程序可以使用部署到 Web 服务器的 WCF RIA 服务。 | [开发和部署 WCF Data Services](/dotnet/framework/data/wcf/developing-and-deploying-wcf-data-services) |
| **LightSwitch** | 自 Visual Studio 2017 起不再支持 LightSwitch，但仍可以从 Visual Studio 2015 及更早版本中部署它。 | [部署 LightSwitch 应用程序](/previous-versions/ff872288(v=vs.140)) |