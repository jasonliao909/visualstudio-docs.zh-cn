---
title: 使用 GitHub Actions 部署到 Azure
description: 了解如何使用 Visual Studio 创建的 GitHub Actions 工作流将应用程序部署到 Azure
ms.date: 09/03/2021
ms.topic: how-to
helpviewer_keywords:
- deployment, GitHub Actions
- GitHub Actions, publish
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
monikerRange: '>= vs-2019'
ms.workload:
- multiple
ms.openlocfilehash: 43a6d56f5088dc542987cb7b850d511b80955698
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665166"
---
# <a name="deploy-your-application-to-azure-using-github-actions-workflows-created-by-visual-studio"></a>使用 Visual Studio 创建的 GitHub Actions 工作流将应用程序部署到 Azure

从 Visual Studio 2019 版本 16.11 开始，你可为 GitHub.com 上托管的 .NET 项目创建新的 GitHub 操作工作流。

## <a name="how-does-it-work"></a>它是如何工作的？

在解决方案资源管理器中，右键单击 GitHub.com 托管项目，然后选择“发布”。

![右键单击 >“发布”](./media/solution-explorer-publish.png)

在下一屏幕上，选择“Azure”，然后选择“下一步” 。

![选择“Azure”](./media/wizard-azure.png)

根据[项目类型](#which-project-types-are-supported)，获取可供选择的不同的 Azure 服务列表。 选择一项满足需求的[受支持的 Azure 服务](#which-azure-services-are-supported)。

![为项目选择适当的 Azure 服务](./media/wizard-pick-azure-service.png)

在向导的最后一步，选择“使用 GitHub Actions 工作流的 CI/CD (生成 yml 文件)”，然后选择“完成” 。

![使用 GitHub Actions 工作流的 CI/CD (生成 yml 文件)](./media/wizard-final-step.png)

Visual Studio 会生成新的 GitHub Actions 工作流，并要求你提交它且将其推送到 GitHub.com。

![提交和推送](./media/summary-commit-and-push.png)

如果使用[内置 Git 工具](../version-control/git-with-visual-studio.md#git-changes-window)完成此步骤，Visual Studio 将检测工作流的执行情况。

![工作流正在运行](./media/summary-workflow-running.png)

## <a name="setting-the-github-secrets"></a>设置 GitHub 机密

若要使生成的工作流成功部署到 Azure，可能需要访问[发布配置文件](/azure/app-service/deploy-github-actions?tabs=applevel#configure-the-github-secret) 

![一个 Github 机密](./media/summary-one-github-secret.png)

要成功部署，可能还需要访问[服务主体](/azure/app-service/deploy-github-actions?tabs=userlevel#configure-the-github-secret)。

![两个 Github 机密](./media/summary-two-github-secrets.png)

在任何情况下，Visual Studio 都会尝试为你使用正确的值设置 Github 机密。 如果设置失败，它将通知你，并让你有机会重试。

![Github 机密缺失](./media/summary-one-github-secret-missing.png)

如果无法重新设置机密，Visual Studio 会提供手动获取机密访问权限的机会，让你能够通过 github.com 上的存储库页面完成该过程。

![设置缺少的 Github 机密](./media/summary-set-github-secret.png)

## <a name="which-project-types-are-supported"></a>支持哪些项目类型？

* ASP.NET Core
* ASP.NET 5 及更高版本
* Azure Functions

## <a name="which-azure-services-are-supported"></a>支持哪些 Azure 服务？

* Azure Web 应用
* Azure Functions
* Azure API 管理
