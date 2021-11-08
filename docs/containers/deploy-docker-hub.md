---
title: 将 ASP.NET Core Linux Docker 容器部署到 Docker Hub | Microsoft Docs
description: 了解如何使用 Visual Studio 容器工具将 ASP.NET Core Web 应用部署到 Docker Hub
author: ghogen
manager: jmartens
ms.technology: vs-container-tools
ms.devlang: dotnet
ms.topic: how-to
ms.date: 10/28/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 528a6624b698753e606cbc8ad6a06b619fd9cdca
ms.sourcegitcommit: aff49629012f4d5fa07c75ea0ca5bf53d28aa173
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2021
ms.locfileid: "131662678"
---
# <a name="deploy-to-docker-hub"></a>部署到 Docker Hub

Docker Hub 为映像存储库提供了一种便利的托管服务。 可以轻松地以手动方式从 Visual Studio 部署到 Docker Hub。

## <a name="create-a-docker-account-and-docker-hub-repository"></a>创建 Docker 帐户和 Docker Hub 存储库

如果没有 Docker 帐户，请[注册](https://hub.docker.com/signup) Docker 帐户。

如果没有 Docker Hub 存储库，请在 [Docker Hub](https://hub.docker.com/) 创建一个存储库。

## <a name="publish-the-image-for-a-single-project-to-docker-hub"></a>将单个项目的映像发布到 Docker Hub

1. 右键单击项目节点，然后选择“发布...”。显示部署选项的屏幕随即出现。

   :::moniker range="vs-2019"
   ![部署选项的屏幕截图。](media/container-tools/vs-2019/docker-container-registry.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![部署选项的屏幕截图。](media/container-tools/vs-2022/docker-container-registry.png)
   :::moniker-end

1. 选择“Docker 容器注册表”，然后选择“Docker Hub” 。

   :::moniker range="vs-2019"
   ![屏幕截图显示“发布”对话框 - 选择“Docker Hub”。](media/deploy-docker-hub/container-tools-docker-hub-deploy.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![屏幕截图显示“发布”对话框 - 选择“Docker Hub”。](media/deploy-docker-hub/vs-2022/container-tools-docker-hub-deploy.png)
   :::moniker-end

1. 输入 Docker 凭据。

   :::moniker range="vs-2019"
   ![Docker Hub 对话框的屏幕截图。](media/deploy-docker-hub/container-tools-docker-hub-credentials.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   ![Docker Hub 对话框的屏幕截图。](media/deploy-docker-hub/vs-2022/container-tools-docker-hub-credentials.png)
   :::moniker-end

1. 如果要连接到自己的存储库（不属于组织），请选中“发布到个人存储库”复选框。 如果存储库归组织所有，请清除该复选框，然后输入组织名称。 输入具有要连接到的存储库的访问权限的 Docker 帐户的 Docker 用户名和密码，然后选择“保存”。

   Visual Studio 尝试将映像部署到 Docker Hub。  如果成功，系统将显示“发布”屏幕，其中包含存储库映像的 URL、映像标记、存储库和生成配置（例如，“版本”） 。

   :::moniker range="vs-2019"
   ![“发布”屏幕的屏幕截图。](media/deploy-docker-hub/container-tools-docker-hub-finished.png)
   :::moniker-end
   :::moniker range=">=vs-2022"
   :::image type="content" source="media/deploy-docker-hub/vs-2022/container-tools-docker-hub-finished.png" alt-text="“发布”屏幕的屏幕截图。" lightbox="media/deploy-docker-hub/vs-2022/container-tools-docker-hub-finished.png":::
   :::moniker-end

1. 单击此页上的“发布”按钮即可随时更新该映像。  也可以通过使用 URL 下面的链接来修改或删除配置文件。

## <a name="next-steps"></a>后续步骤

请按照[部署到 Azure 容器注册表](hosting-web-apps-in-docker.md)中的步骤发布到 [Azure 容器注册表](/azure/container-registry/)。

使用 [Azure Pipelines](/azure/devops/pipelines/?view=azure-devops&preserve-view=true) 设置持续集成和持续交付 (CI/CD)。

## <a name="see-also"></a>请参阅

[部署到 Azure 应用服务](deploy-app-service.md)
[Visual Studio 容器工具](./index.yml)。