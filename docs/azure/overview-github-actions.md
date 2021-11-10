---
title: GitHub 操作
description: 了解如何在 Visual Studio 中开发 GitHub Actions
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: overview
ms.date: 10/19/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 581132bb222b3717e8cfbc22b1041ed11123a011
ms.sourcegitcommit: 32fa8ec0b469a7a9a87de25ff769d8d21d9f30d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2021
ms.locfileid: "131898335"
---
# <a name="an-overview-of-the-github-actions-integration-in-visual-studio"></a>Visual Studio 中 GitHub Actions 集成的概述

[GitHub Actions ](https://github.com/features/actions) 是 GitHub 提供的持续集成/持续交付 (CI/CD) 解决方案。 可在 GitHub.com 上免费托管你的代码，并且可使用 GitHub Actions 在进行代码更改时自动生成、测试和部署应用程序。

## <a name="visual-studio-generates-working-github-action-workflows-for-you"></a>Visual Studio 为你生成可正常工作的 GitHub Actions 工作流

如果你的代码库托管在 GitHub.com 上，并且你的部署目标是 Visual Studio 支持的 Azure 托管服务，则你将自动获得为存储库配置 GitHub Actions 的机会。

![显示 CI/CD 发布选项的屏幕截图。](./media/github-actions-deployment-mode.png)

Visual Studio 还通过为你处理应用程序机密来简化此过程。 

首先，在“解决方案资源管理器”中右键单击你的项目，并从上下文菜单中选择“发布”。 有关教程，请参阅[使用 Visual Studio 创建的 GitHub Actions 工作流将应用程序部署到 Azure](../deployment/azure-deployment-using-github-actions.md)。

## <a name="how-do-i-get-my-project-on-githubcom"></a>如何在 GitHub.com 上获取项目？

请参阅[创建新的 Git 存储库](../version-control/git-with-visual-studio.md#create-a-new-git-repository)。

## <a name="see-also"></a>另请参阅

[GitHub Actions 和 .NET](/dotnet/devops/github-actions-overview)