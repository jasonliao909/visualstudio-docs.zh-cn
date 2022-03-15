---
title: 连接的服务
description: 了解如何在 Visual Studio 中添加向 Azure 服务的连接
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: overview
ms.date: 02/15/2022
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: dfaf2a8c07c2af58fa0e15b837ae7ae294585b87
ms.sourcegitcommit: 798a95fd6d03ef30ec034e5a948ea14fb329f592
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2022
ms.locfileid: "139867170"
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

## <a name="connect-your-app-to-azure-services"></a>连接应用到 Azure 服务

使用连接的服务将应用程序连接到实时 Azure 服务仿真器和 Azure 服务的其他本地替代项。 Visual Studio 当前支持以下项：

| 名称 | 说明 |
| - | - |
| [Azure 应用配置](/azure/azure-app-configuration/overview) | 在 Azure 中集中管理的访问密钥-值设置和功能标志。 |
| [Azure App Insights](/azure/azure-monitor/app/app-insights-overview) | 为实时 web 应用提供可扩展的应用程序性能管理和监视。 |
| [Azure 应用服务](/azure/app-service/overview) | 提供实时 web 应用的可缩放的完整服务托管。 |
| [Azure Functions](/azure/azure-functions/functions-overview) | 为 web Api 等提供可缩放的按需计算服务。 |
| [Azure 存储](/azure/storage) | 支持 Blob、表、队列和磁盘的可缩放的云存储空间。 |
| [Azure SignalR 服务](/azure/azure-signalr/signalr-overview) | 基于 HTTP 的实时 Web 功能。 |
| [Azure Key Vault](/azure/key-vault/general/overview) | Azure 应用程序使用的加密密钥和其他机密的安全云存储空间。 |
| [Azure SQL 数据库](/azure/azure-sql) | 云托管 SQL 数据库。 |
| [用于 Redis 的 Azure 缓存](/azure/azure-cache-for-redis/cache-overview)| 基于 Redis 软件的内存中数据存储。 |
| [Azure Cosmos DB](/azure/cosmos-db/introduction) | 一种完全托管的 NoSQL 数据库，用于新式应用开发。| 
| [Microsoft 标识平台](/azure/active-directory/develop/v2-overview) | 使用 Microsoft 标识和社交帐户进行身份验证。 |

> [!NOTE]
> 使用“发布”，可将应用程序部署到 Azure 托管服务，例如 Azure VM、Azure 应用服务、Azure Functions 和 Azure 容器注册表

## <a name="support-for-azure-emulators-and-local-alternatives"></a>支持 Azure 仿真器和本地替代项

Visual Studio 通过简化从本地仿真的服务到云中运行的服务的转换，使得在本地开发 Azure 应用程序变得更加容易。 你可以使用连接的服务将应用程序连接到本地模拟器，其中某些模拟器在本地容器中运行，其他本地替代 Azure 服务。 Visual Studio 当前支持以下项：

| 名称 | 说明 |
| - | - |
| [容器上的 Azure CosmosDB Emulator](/azure/cosmos-db/introduction) | 在本地容器中运行的 Azure CosmosDB 模拟器。 |
| [Azure 存储仿真程序](/azure/storage/common/storage-use-azurite?toc=%2Fazure%2Fstorage%2Fblobs%2Ftoc.json&tabs=visual-studio) | Azurite 是在本地计算机上运行的 Azure 存储仿真器。 |
| [Application Insights SDK](/azure/azure-monitor/app/app-insights-overview) | Application Insights 服务的本地模式。  |
| [容器上的 MongoDB](/azure/cosmos-db/introduction) | MongoDB 文档数据库提供高可靠性和可伸缩性。 此选项使其在本地容器中可用。 |
| [容器上的 PostgreSQL](/azure/postgresql/overview) | PostgreSQL 是一个对象关系数据库系统，可提供可靠性和数据完整性。 此选项使其在本地容器中可用。 |
| [容器上的 RabbitMQ](/azure/azure-functions/functions-bindings-rabbitmq) | RabbitMQ 是一种开放源多协议消息代理。 此选项使其在本地容器中可用。 |
| [容器上的 Redis 缓存](/azure/azure-cache-for-redis/cache-overview) | 托管在本地容器中的 Redis 缓存。 |
| [SQLite](/ef/core/providers/sqlite/?tabs=dotnet-core-cli) | SQLite 是一个进程内库，它提供无配置的自包含事务性 SQL 数据库引擎。 |
| [SQL Server 数据库](/sql/sql-server/) | 本地 SQL Server Database。 |
| [SQL Server Express LocalDB](/sql/database-engine/configure-windows/sql-server-express-localdb) | Azure SQL 数据库的本地替代项。 |
| [Secrets.json](/aspnet/core/security/app-secrets?tabs=windows) | Key Vault 的本地替代项。 |

## <a name="how-it-works"></a>工作原理

Visual Studio 在解决方案资源管理器中的“属性”下创建了两个名为 serviceDependencies.json 和 serviceDependencies.local.json 的可见新文件 。 这两个文件都可安全地签入，因为它们不包含任何机密。

Visual Studio 还会创建一个名为 serviceDependencies.local.json.user 的文件，它默认在解决方案资源管理器中不可见。 此文件包含可能被视为机密的信息（例如 Azure 中的资源 ID），我们建议你不要签入它。

## <a name="containers"></a>容器

连接的服务可帮助你运行在容器中本地仿真 Azure 服务的应用程序依赖项。 例如，你可以在本地的容器中运行名为 Azurite 的 Azure 存储模拟器。 下一节介绍 Visual Studio 提供的支持，用于在容器中使用这些模拟服务时使用 Azure 中运行的实际服务。

## <a name="local-and-connected-configurations"></a>本地配置和连接配置

在开发过程中，通常使用本地模拟器、本地数据库或在本地容器中运行的模拟服务。 当你使用 Visual Studio 中的发布过程来部署到云时，无论是 Azure、Docker 中心还是其他受支持的远程环境，Visual Studio 都可以指导你完成到连接到实际服务和数据库的转换。 当你在 **解决方案资源管理器** 中右键单击项目节点并选择 " **发布**" 时，会指导你将应用部署到云，但此后，你先前为本地使用配置的服务相关性现在会显示在连接的服务 UI 中，其中包含黄色的警告图标和 **配置** 链接：

![显示 "连接的服务" 选项卡中的 "配置" 选项的屏幕截图。](media/vs-2022/configure-service-dependencies.png)

如果单击这些链接，Visual Studio 将显示一些屏幕，要求在云中运行的 "真实" 服务（而不是本地服务）连接信息。 例如，如果最初将应用配置为使用本地运行的 SQL LocalDB 实例运行，则你已提供连接字符串名称和引用该数据库LocalDB值。 首次将应用部署到云环境后，可以使用"配置链接"指定在云中使用的连接字符串。 对于 Azure 部署Visual Studio，还可以选择使用 Azure Key Vault安全地存储连接字符串和其他机密。[](/azure/key-vault/general/overview)

![显示用于将服务替换为实际SQL LocalDB连接的选项的屏幕截图。](media/vs-2022/configure-dependency.png)