---
title: 发布到 Azure 应用服务
description: 了解将 ASP.NET、ASP.NET Core、Node.js 和 .NET Core 应用发布到 Azure 应用服务或 Azure 应用服务 Linux 的方法。
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
- azure
ms.openlocfilehash: 53c14db342e48ceccc7651220ac86c8bcacedcf3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122146272"
---
# <a name="publish-a-web-app-to-azure-app-service-using-visual-studio"></a>使用 Visual Studio 将 Web 应用发布到 Azure 应用服务

对于 ASP.NET、ASP.NET Core、Node.js 和 .NET Core 应用，请使用以下任一方法发布到 Azure 应用服务或 Azure 应用服务 Linux（使用容器）。

* 对于应用的连续（或自动）部署，请将 Azure DevOps 与 [Azure 管道](/azure/devops/pipelines/get-started-yaml?view=azdevops&preserve-view=true)结合使用。

* 对于应用的一次性（或手动）部署，请使用 Visual Studio 中的“发布”工具将 ASP.NET、ASP.NET Core、Node.js 和 .NET Core 应用部署到 Azure 应用服务或[适用于 Linux 的应用服务](../deployment/quickstart-deploy-to-linux.md)（使用容器）。 对于 Python 应用，请按照 [Python - 发布到 Azure 应用服务](../python/publishing-python-web-applications-to-azure-from-visual-studio.md)上的步骤操作。

本文介绍如何使用“Publish”工具进行一次性部署。

[!INCLUDE [quickstart-prereqs-azure](includes/quickstart-prereqs-azure.md)]

## <a name="publish-to-azure-app-service-on-windows"></a>发布到 Windows 上的 Azure 应用服务

1. 在解决方案资源管理器中，右键单击该项目节点，并选择“发布”（或使用“生成” > “发布”菜单项）  。

    ![解决方案资源管理器中项目上下文菜单上的“发布”命令](../deployment/media/quickstart-publish.png "选择发布")

1. 如果先前配置了任何发布配置文件，则“发布”窗口会显示。 选择“新建”。

1. 在“发布”窗口中，选择“Azure”。

    ![选择发布目标](../deployment/media/quickstart-publish-azure-new.png)

1. 选择“Azure 应用服务(Windows)”，然后选择“下一步” 。

    ![选择“Linux 上的 Azure 应用服务”](../deployment/media/quickstart-publish-windows-select-azure-service.png)

1. 如有必要，请用 Azure 帐户登录。 选择“创建新的 Azure 应用服务…”

    ![用于创建新的 Azure 应用服务实例的链接](../deployment/media/quickstart-publish-windows-create-new-link.png)

1. 在“创建 Azure 应用服务(Windows)”对话框中，填写“应用名称”、“资源组”和“应用服务计划”输入字段   。 可以保留这些名称，也可以进行更改。 准备就绪后，选择“创建”。

    ![“创建 Azure 应用服务(Windows)”对话框的屏幕截图，其中已填写“名称”、“订阅”、“资源组”和“托管计划”字段。](../deployment/media/quickstart-publish-windows-create-new-dialog.png)

1. 在“发布”对话框中，将自动选择新创建的实例。 准备就绪后，选择“完成”。

    ![从 Visual Studio 解决方案资源管理器访问的“发布”窗口的屏幕截图。 选择 Azure 作为发布目标。](../deployment/media/quickstart-publish-windows-select-instance.png)

1. 选择“发布”。 Visual Studio 将应用部署到 Azure 应用服务，并且 Web 应用将在浏览器中加载。 项目属性“发布”窗格显示了站点 URL 和其他详细信息。

    ![显示配置文件摘要的“发布”属性窗格](../deployment/media/quickstart-publish-windows-summary-page.png)

## <a name="clean-up-resources"></a>清理资源

在前面的步骤中，你在资源组中创建了 Azure 资源。 如果以后不需要这些资源，可以通过删除资源组来删除它们。
从 Azure 门户左侧菜单中，选择“资源组”，然后选择“myResourceGroup” 。
在资源组页上，确保列出的资源是要删除的。
选择“删除”，在文本框中键入“myResourceGroup”，然后选择“删除”  。

## <a name="next-steps"></a>后续步骤

在本快速入门中，学习了如何使用 Visual Studio 创建用于部署到 Azure 的发布配置文件。 还可以通过从 Azure 应用服务导入发布设置来配置发布配置文件。

> [!div class="nextstepaction"]
> [导入发布设置并部署到 Azure](tutorial-import-publish-settings-azure.md)
