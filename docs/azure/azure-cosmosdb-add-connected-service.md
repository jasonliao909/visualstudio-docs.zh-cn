---
title: 使用连接服务添加 Azure Cosmos DB | Microsoft Docs
description: 通过使用 Visual Studio 添加连接服务，向应用添加 Azure Cosmos DB 支持
author: AngelosP
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 69e6fa19c1f89f5756096cfd41e533857df47476
ms.sourcegitcommit: 8671132ee0425b273b060fa35c75657e7ae02583
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2021
ms.locfileid: "132924168"
---
# <a name="add-azure-cosmos-db-to-your-app-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接服务将 Azure Cosmos DB 添加到你的应用

在 Visual Studio 中，通过使用“连接服务”功能可将以下任何服务连接到 Azure Cosmos DB：

- .NET Framework 控制台应用
- ASP.NET MVC (.NET Framework) 
- ASP.NET Core
- .NET Core（包括控制台应用、WPF、Windows 窗体、类库）
- .NET Core 辅助角色
- Azure Functions
- 通用 Windows 平台应用
- Xamarin
- Cordova

连接服务功能可将所有需要的引用和连接代码添加到项目，并相应地修改配置文件。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中连接服务](/visualstudio/mac/connected-services)。
## <a name="prerequisites"></a>先决条件

- 安装有 Azure 工作负荷的 Visual Studio。
- 一个受支持类型的项目

## <a name="connect-to-azure-cosmos-db-using-connected-services"></a>使用连接服务连接到 Azure Cosmos DB

1. 在 Visual Studio 中打开项目。

1. 在“解决方案资源管理器”中，右键单击“连接服务”节点，并在上下文菜单中选择“添加连接服务”。

1. 在“连接服务”选项卡中，选择“服务依赖项”的 + 图标。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在“添加依赖项”页中，选择“Azure Cosmos DB”。

    ![添加 Azure Cosmos DB](./media/azure-cosmosdb-add-connected-service/azure-cosmosdb.png)

    如果你还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/)。

1. 在“Azure Cosmos DB”屏幕中，选择现有的 Azure Cosmos DB，然后选择“下一步”。

    如果需要创建数据库，请转到下一步。 否则，请跳到步骤 7。

    ![将现有 Cosmos DB 添加到项目中](./media/azure-cosmosdb-add-connected-service/created-cosmosdb.png)

1. 创建 Azure Cosmos DB：

   1. 选择屏幕底部的“新建 Azure Cosmos DB”。

   1. 填写“Azure Cosmos DB: 新建”屏幕，然后选择“创建”。

       ![新的 Azure Cosmos DB](./media/azure-cosmosdb-add-connected-service/create-new-cosmosdb.png)

   1. 当显示“配置 Azure Cosmos DB”屏幕时，新数据库将出现在列表中。 在列表中选择新数据库，并选择“下一步”。

1. 输入连接字符串名称，然后选择是要将连接字符串存储在本地机密文件中还是存储在 [Azure Key Vault](/azure/key-vault) 中。

   ![指定连接字符串](./media/azure-cosmosdb-add-connected-service/connection-string.png)

1. “更改摘要”屏幕显示了在完成该过程后将对项目进行的所有修改。 如果更改看起来正常，请选择“完成”。

   ![更改摘要](./media/azure-cosmosdb-add-connected-service/summary-of-changes.png)

1. 连接显示在“连接服务”选项卡的“服务依赖项”部分下。

   ![服务依赖项](./media/azure-cosmosdb-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure Cosmos DB 产品页](https://azure.microsoft.com/services/cosmos-db/)
- [Azure Cosmos DB 文档](/azure/cosmos-db/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
