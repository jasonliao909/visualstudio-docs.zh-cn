---
title: 发布到网站
description: 了解如何使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到网站。
ms.custom: SEO-VS-2020
ms.date: 01/29/2019
ms.topic: quickstart
helpviewer_keywords:
- deployment, website
ms.assetid: fc82b1f1-d342-4b82-9a44-590479f0a895
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 17cd220c3c04c36f0870f6644b63a3abb190f81a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127839"
---
# <a name="publish-a-web-app-to-a-web-site-using-visual-studio"></a>使用 Visual Studio 将 Web 应用发布到网站

可以使用“发布”工具将 ASP.NET、ASP.NET Core、.NET Core 和 Python 应用从 Visual Studio 发布到网站。 对于 Node.js，支持这些步骤但用户界面不同。

[!INCLUDE [quickstart-prereqs](includes/quickstart-prereqs.md)]

> [!NOTE]
> 如果需要将 Windows 桌面应用程序发布到网络文件共享，请参阅[使用 ClickOnce 部署桌面应用](how-to-publish-a-clickonce-application-using-the-publish-wizard.md)（C# 或 Visual Basic）。 对于 C++/CLR，请参阅[使用 ClickOnce 部署本机应用](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)，或者对于 C/C++，请参阅[使用安装项目部署本机应用](/cpp/windows/walkthrough-deploying-a-visual-cpp-application-by-using-a-setup-project)。

## <a name="publish-to-a-web-site"></a>发布到网站

1. 在解决方案资源管理器中，右键单击该项目并选择“发布”（或使用“生成” > “发布”菜单项）  。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择发布")

1. 如果先前配置了任何发布配置文件，则“发布”窗格会显示。 选择“新建”。

1. 在“发布”窗口中，选择“Web 服务器(IIS)”。

    ![选择发布目标](../deployment/media/quickstart-publish-iis.png "选择 IIS、FTP 等。")

1. 选择“Web 部署”作为部署方法。 Web 部署简化了将 Web 应用程序和网站部署到 IIS 服务器的过程，并且必须作为应用程序安装在服务器上。 使用 [Web 平台安装程序](https://www.microsoft.com/web/downloads/platform.aspx)进行安装。

    ![选择部署方法](../deployment/media/quickstart-publish-iis-web-deploy.png "选择 IIS、FTP 等。")

1. 为发布方法配置所需设置，并选择“完成”。 

    ![Web 部署连接详细信息](../deployment/media/quickstart-publish-iis-web-deploy-connection-details.png)

1. 要进行发布，请选择摘要页面中的“发布”。 “输出”窗口显示部署进度和结果。

   有关如何对 IIS 上的 ASP.NET Core 进行故障排除的帮助，请参阅[对 Azure 应用服务和 IIS 上的 ASP.NET Core 进行故障排除](/aspnet/core/test/troubleshoot-azure-iis)。

## <a name="next-steps"></a>后续步骤

在本快速入门中，学习了如何使用 Visual Studio 创建发布配置文件。 此外可以通过导入发布设置来配置发布配置文件。

> [!div class="nextstepaction"]
> [导入发布设置并部署到 IIS](tutorial-import-publish-settings-iis.md)
