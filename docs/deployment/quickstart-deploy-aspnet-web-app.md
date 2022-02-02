---
title: 发布 ASP.NET Web 应用
description: 了解如何使用“发布”工具将 ASP.NET 和 ASP.NET Core 从 Visual Studio 发布到网站。
ms.date: 01/30/2022
ms.topic: quickstart
ms.custom: devdivchpfy22
helpviewer_keywords:
- deployment, web app
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 4ad4c0a5b9c663f4daf02dbe8de8826ac31926dd
ms.sourcegitcommit: 3766c051f9a8b35106b16f751db7fecde0b92254
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "137951608"
---
# <a name="quickstart-publish-an-aspnet-web-app"></a>快速入门：发布 ASP.NET Web 应用

在本文中，你将了解如何将第一个 ASP.NET web 应用发布到各种位置，包括诸如 IIS 和远程云环境（如 Azure App Service）的各种位置。

本文支持 ASP.NET 和 ASP.NET Core。

## <a name="prerequisites"></a>先决条件

你需要已安装 ASP.NET 和 Web 开发工作负载的 [Visual Studio](https://www.visualstudio.com/downloads)。

如果已安装 Visual Studio：

* 通过选择“帮助” > “检查更新”，在 Visual Studio 中安装最新更新。
* 通过选择“工具” > “获取工具和功能”，添加工作负荷。

## <a name="get-started"></a>入门

在解决方案资源管理器中，右键单击项目，选择“发布”。

![右键单击并发布](./media/right-click-publish.png)

如果是首次发布此 web 应用，请在下一步中看到发布向导。

![发布向导 - 发布目标](./media/publish-targets-general.png)

> [!NOTE]
> Visual Studio 根据 web 应用的类型筛选目标列表。

## <a name="azure"></a>[Azure](#tab/azure)
## <a name="publish-your-web-app-to-azure"></a>将 Web 应用发布到 Azure

有关发布 web 应用的详细步骤，请参阅[快速入门：部署 ASP.NET 的 web 应用](/azure/app-service/quickstart-dotnetcore?tabs=netcore31&pivots=development-environment-vs#publish-your-web-app)。

## <a name="docker"></a>[Docker](#tab/docker)
## <a name="publish-your-web-app-to-docker-container-registry"></a>将 Web 应用发布到 Docker 容器注册表

可以将 Web 应用作为 Docker 容器发布到任何兼容的 Docker 容器注册表。

![突出显示发布到 Docker 容器注册表](./media/publish-docker-container-registry-highlighted.png)

单击“下一步”，然后从可用选项中进行选择，例如 Azure 容器注册表或 Docker Hub。

![发布到 Docker 容器注册表选项](./media/publish-docker-container-registry-options.png)

### <a name="azure-container-registry"></a>Azure 容器注册表

接下来，对于 Azure 容器注册表，要么选择一个现有的实例，要么创建一个新实例。

![发布到 Azure 容器注册表](./media/publish-acr-select-instance.png)

### <a name="docker-hub"></a>Docker Hub

接下来，对于 Docker Hub，请提供发布凭据。

![发布到 Docker Hub](./media/publish-dockerhub-details.png)

### <a name="other-docker-container-registry"></a>其他 Docker 容器注册表

接下来，对于其他 Docker 容器注册表，请提供 URI 和发布凭据。

![发布到其他 Docker 容器注册表](./media/publish-custom-docker-registry-details.png)

### <a name="finish-the-publish-wizard"></a>完成发布向导

接下来，你将看到刚刚使用发布向导创建的新[发布配置文件](./publish-overview.md)的摘要页面。 单击“发布”，Visual Studio 会将 Web 应用部署到指定的 Docker 容器注册表。

![发布到 Docker 容器注册表 - 摘要页面](./media/publish-docker-container-registry-summary-page.png)

> [!NOTE]
> 上面的屏幕截图显示了面向 Azure Docker 注册表的发布配置文件，但同一个“发布”按钮可用于所有三个 Docker 容器注册表选项。

## <a name="folder"></a>[文件夹](#tab/folder)
## <a name="publish-your-web-app-to-a-folder"></a>将 Web 应用发布到文件夹

可以将 Web 应用发布到本地和网络文件夹。

![突出显示发布到文件夹](./media/publish-folder-highlighted.png)

首先，提供路径，然后单击“完成”以完成发布向导。

![发布到文件夹](./media/publish-folder.png)

接下来，你将看到刚刚使用发布向导创建的新[发布配置文件](./publish-overview.md)的摘要页面。 单击“发布”，Visual Studio 会将 Web 应用部署到提供的路径。

![发布到文件夹 - 摘要页面](./media/publish-folder-summary-page.png)

关闭后，可以返回到该摘要页面。 下次右键单击并选择“发布”时，Visual Studio 会打开此摘要页面。 （若要返回到发布向导，只需单击摘要页面中的“新建”即可。）

## <a name="ftpftps"></a>[FTP/FTPS](#tab/ftp-ftps)
## <a name="publish-your-web-app-to-an-ftpftps-server"></a>将 Web 应用发布到 FTP/FTPS 服务器

你可以使用 FTP 或 FTPS 发布 Web 应用。

![发布到 FTP 或 FTPS 服务器](./media/publish-ftp.png)

提供必要的连接详细信息，然后选择“完成”。

![发布到 FTP 或 FTPS 服务器 - 详细信息](./media/publish-ftp-details-latest.png)

接下来，你将看到刚刚使用发布向导创建的新[发布配置文件](./publish-overview.md)的摘要页面。 单击“发布”，Visual Studio 会将 Web 应用部署到提供的 FTP 或 FTPS 服务器。

![发布到 FTP 或 ftps 服务器 - 摘要页面](./media/publish-ftp-summary-page.png)

关闭后，可以返回到该摘要页面。 下次右键单击并选择“发布”时，Visual Studio 会打开此摘要页面。 （若要返回到发布向导，只需单击摘要页面中的“新建”即可。）

## <a name="web-server"></a>[Web 服务器](#tab/web-server)
## <a name="publish-your-web-app-to-web-server-iis"></a>将 Web 应用发布到 Web 服务器 (IIS)

你可以将 Web 应用发布到 IIS。

![发布到 IIS](./media/publish-iis.png)

选取所需的部署模式 (如果不确定，请使用默认) 。

![发布到 IIS - 部署模式](./media/publish-iis-deployment-mode.png)

### <a name="web-deploy"></a>Web Deploy

提供必要的连接详细信息，然后选择“完成”。

![发布到 IIS - Web 部署](./media/publish-iis-web-deploy-latest.png)

### <a name="web-deploy-package"></a>Web 部署包

单击“浏览...”以打开“选择包位置”对话框，并输入要创建包的路径，包括 .zip文件名称。

![发布到 IIS - Web 部署包](./media/publish-iis-web-deploy-package.png)

### <a name="finish-the-publish-wizard"></a>完成发布向导

接下来，你将看到刚刚使用发布向导创建的新[发布配置文件](./publish-overview.md)的摘要页面。 单击“发布”，Visual Studio 会将 Web 应用部署到指定的 IIS 服务器。

![发布到 IIS - 摘要页面](./media/publish-iis-web-deploy-package-summary-page.png)

## <a name="import-profile"></a>[导入配置文件](#tab/import-profile)
## <a name="import-profile"></a>导入配置文件

你可以[从 IIS](./tutorial-import-publish-settings-iis.md) 和 [Azure 应用服务](./tutorial-import-publish-settings-azure.md#create-the-publish-settings-file-in-azure-app-service)导入发布设置

---