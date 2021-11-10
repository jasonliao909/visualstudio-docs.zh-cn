---
title: 连接的服务
description: 了解如何在 Visual Studio 中添加向 Azure 服务的连接
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: overview
ms.date: 10/19/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: 2470c410eb2fff1da54343b139b80dc93f2c37a1
ms.sourcegitcommit: 32fa8ec0b469a7a9a87de25ff769d8d21d9f30d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2021
ms.locfileid: "131898333"
---
# <a name="overview-connected-services"></a>概述：连接的服务

连接的服务是 Visual Studio 中的一个工具集合，可帮助你将应用程序连接到以下项：

* Azure 服务
* OpenAPI 终结点
* gRPC（远程过程调用）终结点
* Windows Communication Foundation (WCF) 终结点

首先，右键单击解决方案资源管理器中的“连接的服务”节点，然后选择“管理连接的服务” 。

支持的项目类型因服务类型而异。 你将在列出的选择中看到适用于你的项目类型的选项。

## <a name="connect-your-app-to-grpc-openapi-and-wcf-endpoints"></a>将应用连接到 gRPC、OpenAPI 和 WCF 终结点

使用连接的服务将应用程序连接到以下任一服务：

| 名称 | ASP.NET 链接 | 说明 |
|-|-|-|
| [OpenAPI](https://github.com/OAI/OpenAPI-Specification) 终结点 | [使用 OpenAPI 开发 ASP.NET Core 应用](/aspnet/core/web-api/Microsoft.dotnet-openapi) | 一种标准格式，用于以计算机可读和人类可读的形式描述服务的功能。 |
| [gRPC](https://grpc.io/docs/) 终结点 | [.NET 上的 gRPC 服务简介](/aspnet/core/grpc/) | 一种开源实时过程调用服务。 |
| [WCF](/dotnet/framework/wcf/) 终结点 | 不适用 | 一种 .NET Framework 解决方案，支持使用分布式服务网络进行编程。 |

Visual Studio 将生成任何必要的客户端或服务器代码来简化通信。

## <a name="connect-your-app-azure-services"></a>将应用与 Azure 服务连接

使用连接的服务将应用程序连接到实时 Azure 服务仿真器和 Azure 服务的其他本地替代项。 Visual Studio 当前支持以下项：

| 名称 | 说明 |
| - | - |
| [Azure 存储](/azure/storage) | 支持 Blob、表、队列和磁盘的可缩放的云存储空间。 |
| [Azure SignalR 服务](/azure/azure-signalr/signalr-overview) | 基于 HTTP 的实时 Web 功能。 |
| [Azure Key Vault](/azure/key-vault/general/overview) | Azure 应用程序使用的加密密钥和其他机密的安全云存储空间。 |
| [Azure SQL 数据库](/azure/azure-sql) | 云托管 SQL 数据库。 |
| [用于 Redis 的 Azure 缓存](/azure/azure-cache-for-redis/cache-overview)| 基于 Redis 软件的内存中数据存储。 |
| [Azure Cosmos DB](/azure/cosmos-db/introduction) | 一种完全托管的 NoSQL 数据库，用于新式应用开发。| 
| [Azure Microsoft 标识平台](/azure/active-directory/develop/v2-overview) | 使用 Microsoft 标识和社交帐户进行身份验证。 |

> [!NOTE]
> 使用“发布”，可将应用程序部署到 Azure 托管服务，例如 Azure VM、Azure 应用服务、Azure Functions 和 Azure 容器注册表

## <a name="support-for-azure-emulators-and-local-alternatives"></a>支持 Azure 仿真器和本地替代项

Visual Studio 通过简化从本地仿真的服务到云中运行的服务的转换，使得在本地开发 Azure 应用程序变得更加容易。 可使用连接的服务将应用程序连接到本地仿真器和 Azure 服务的其他本地替代项。 Visual Studio 当前支持以下项：

| 名称 | 说明 |
| - | - |
| [Azure 存储仿真程序](/azure/storage/common/storage-use-azurite?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=visual-studio) | Azurite 是在本地计算机上运行的 Azure 存储仿真器。 |
| [Application Insights SDK](/azure/azure-monitor/app/app-insights-overview) | Application Insights 服务的本地模式。  |
| [SQL Server Express LocalDB](/sql/database-engine/configure-windows/sql-server-express-localdb) | Azure SQL 数据库的本地替代项 |
| [Secrets.json](/aspnet/core/security/app-secrets?tabs=windows) | Key Vault 的本地替代项 |

## <a name="containers"></a>容器

连接的服务可帮助你运行在容器中本地仿真 Azure 服务的应用程序依赖项。 可在容器中本地运行名为 Azurite 的 Azure 存储仿真器。 也可在容器中本地运行 Redis，以仿真 Azure Cache for Redis。

## <a name="how-it-works"></a>工作原理

Visual Studio 在解决方案资源管理器中的“属性”下创建了两个名为 serviceDependencies.json 和 serviceDependencies.local.json 的可见新文件 。 这两个文件都可安全地签入，因为它们不包含任何机密。

Visual Studio 还会创建一个名为 serviceDependencies.local.json.user 的文件，它默认在解决方案资源管理器中不可见。 此文件包含可能被视为机密的信息（例如 Azure 中的资源 ID），我们建议你不要签入它。

