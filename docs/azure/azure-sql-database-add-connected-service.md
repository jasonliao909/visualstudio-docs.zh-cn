---
title: 将连接添加到Azure SQL 数据库 |Microsoft Docs
description: 使用Azure SQL 数据库添加与应用的连接Visual Studio 连接的服务
author: AngelosP
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: 231951c261f8a2df75c743ef9b6af96397520871
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129430581"
---
# <a name="add-a-connection-to-azure-sql-database"></a>将连接添加到Azure SQL 数据库

使用 Visual Studio，可以使用 连接的服务 功能将以下任何Azure SQL 数据库连接到 **连接的服务：**

- .NET Framework控制台应用
- ASP.NETMVC (.NET Framework)  
- ASP.NET Core
- .NET Core (包括控制台应用、WPF、Windows窗体、类库) 
- .NET Core 辅助角色
- Azure Functions
- 通用Windows平台应用
- Xamarin
- Cordova

连接服务功能可将所有需要的引用和连接代码添加到项目，并相应地修改配置文件。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中连接服务](/visualstudio/mac/connected-services)。
## <a name="prerequisites"></a>先决条件

- Visual Studio已安装 Azure 工作负载。
- 支持的类型之一的项目

## <a name="connect-to-azure-sql-database-using-connected-services"></a>连接Azure SQL 数据库连接的服务

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器** 中，右键单击连接的服务节点，然后从上下文菜单中选择"**添加连接的服务"。**

1. 在 **"连接的服务"** 选项卡中，选择"服务依赖项 **"的"+"图标**。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在"**添加依赖项"页** 中，选择 **"Azure SQL 数据库"。**

    ![添加Azure SQL 数据库服务](./media/azure-sql-database-add-connected-service/azure-sql-database.png)

    如果还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/)。

1. 在"**配置Azure SQL 数据库"** 屏幕中，选择现有Azure SQL 数据库，然后选择"下一 **步"。**

    如果需要创建新组件，请转到下一步。 否则，请跳到步骤 7。

    ![连接现有Azure SQL 数据库组件](./media/azure-sql-database-add-connected-service/created-azure-sql-database.png)

1. 若要创建Azure SQL 数据库：

   1. 选择 **屏幕SQL 数据库** 创建一个窗口。

   1. 填写 **"Azure SQL 数据库：创建新屏幕**"，然后选择"创建 **"。**

       ![新Azure SQL 数据库](./media/azure-sql-database-add-connected-service/create-new-azure-sql-database.png)

   1. 显示 **"配置Azure SQL 数据库"** 屏幕时，新数据库将显示在列表中。 在列表中选择新数据库，然后选择"下一 **步"。**

1. 输入连接字符串名称或选择默认值，然后选择是希望连接字符串存储在本地机密文件中， [还是](/azure/key-vault)存储在 Azure Key Vault。

   ![指定连接字符串](./media/azure-sql-database-add-connected-service/connection-string.png)

1. " **更改摘要** "屏幕显示完成该过程后对项目所做的所有修改。 如果更改看起来正常，请选择"完成 **"。**

   ![更改摘要](./media/azure-sql-database-add-connected-service/summary-of-changes.png)

   如果系统提示设置防火墙规则，请选择"**是"。**

   ![防火墙规则](./media/azure-sql-database-add-connected-service/firewall-rules.png)

1. 连接显示在"连接 **"选项卡的** "服务依赖项 **"连接的服务** 下。

   ![服务依赖项](./media/azure-sql-database-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure SQL 数据库产品页](https://azure.microsoft.com/services/sql-database/)
- [Azure SQL 数据库文档](/azure/azure-sql/database/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
