---
title: 发布概述
description: 了解 Visual Studio 中的“发布”窗口
ms.date: 10/14/2021
ms.topic: overview
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Publish tool
- .NET applications, publishing
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: '>= vs-2019'
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4eefc0c2d4122d3e9b6b96f026fb9f823bb52dbd
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131128717"
---
# <a name="overview-of-publish"></a>发布概述

针对 ASP.NET、.NET Core 和 Python 应用，可以使用“发布”工具来部署你的应用程序。

## <a name="what-is-publish"></a>什么是“发布”工具？

“发布”工具可帮助将应用程序部署到各种目标。 在“解决方案资源管理器”中右键单击项目，并从上下文菜单中选择“发布”，即可开始使用。

## <a name="how-does-it-work"></a>它是如何工作的？

发布使用配置文件（.pubxml 文件）来允许多个项目配置和单个项目的多个发布目标。

![发布配置文件](./media/publish-profiles.png)

配置文件的内容为 XML，并基于 MSBuild。

![发布配置文件示例内容](./media/publish-profile-example-contents.png)

发布配置文件将凭据保留为单独的文件，该文件默认隐藏，不会签入。

![隐藏用户文件](./media/separate-user-files.png)

始终可以[从 IIS](../deployment/tutorial-import-publish-settings-iis.md#create-the-publish-settings-file-in-iis-on-windows-server) 和 [Azure 应用服务](../deployment/tutorial-import-publish-settings-azure.md#create-the-publish-settings-file-in-azure-app-service)导入发布配置文件

![导入配置文件](./media/import-profile.png)

## <a name="visual-studio-can-help-you-manage-dependencies-to-azure-services"></a>Visual Studio 可帮助管理 Azure 服务的依赖项

使用“发布”工具将应用程序部署到 Azure 时，有机会配置 Azure 服务的依赖项。

![发布期间的依赖项](./media/publish-dependencies.png)

你可能希望连接到不同的 SQL 数据库、不同的存储帐户或不同的密钥保管库，以使用不同的环境，例如测试、QA、预生产等。
