---
title: 使用 Azure Cache for Redis 添加连接的服务 |Microsoft Docs
description: 使用Azure Cache for Redis添加连接服务，Visual Studio应用添加支持
author: AngelosP
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: a8c234db5d9b0f003fa269def46b8c3fcc3da164
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129430708"
---
# <a name="add-azure-cache-for-redis-by-using-visual-studio-connected-services"></a>使用 Azure Cache for Redis 添加Visual Studio 连接的服务

使用 Visual Studio，可以使用 连接的服务 功能将以下任一项连接到 **Azure Cache for Redis：**

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

## <a name="connect-to-azure-cache-for-redis-using-connected-services"></a>连接 Azure Cache for Redis 连接的服务

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器** 中，右键单击连接的服务节点，然后从上下文菜单中选择"**添加连接的服务"。**

1. 在 **"连接的服务"** 选项卡中，选择"服务依赖项 **"的"+"图标**。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在"**添加依赖项"页** 中，选择 **"Azure Cache for Redis"。**

    ![添加 Azure Cache for Redis](./media/azure-redis-cache-add-connected-service/azure-redis-cache.png)

    如果还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/)。

1. 在"**配置Azure Cache for Redis"** 屏幕中，选择现有Azure Cache for Redis，然后选择"下一 **步"。**

    如果需要创建新组件，请转到下一步。 否则，请跳到步骤 7。

    ![连接现有Azure Cache for Redis](./media/azure-redis-cache-add-connected-service/created-azure-redis-cache.png)

1. 若要创建 Azure Redis 缓存，请执行：

   1. 选择 **屏幕底部的"创建新的 Azure Redis** 缓存"。

   1. 填写 **"Azure Cache for Redis：创建新屏幕**"，然后选择"创建 **"。**

       ![新Azure Cache for Redis](./media/azure-redis-cache-add-connected-service/create-new-azure-redis-cache.png)

   1. 显示 **"配置Azure Cache for Redis"** 屏幕时，新缓存将显示在列表中。 在列表中选择新数据库，然后选择"下一 **步"。**

1. 输入连接字符串名称，或选择默认值，然后选择是希望连接字符串存储在本地机密文件中， [还是](/azure/key-vault)存储在 Azure Key Vault。

   ![指定连接字符串](./media/azure-redis-cache-add-connected-service/connection-string.png)

1. " **更改摘要** "屏幕显示完成该过程后对项目所做的所有修改。 如果更改看起来正常，请选择"完成 **"。**

   ![更改摘要](./media/azure-redis-cache-add-connected-service/summary-of-changes.png)

1. 连接显示在"连接 **"选项卡的** "服务依赖项 **"连接的服务** 下。

   ![服务依赖项](./media/azure-redis-cache-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure Cache for Redis产品页](https://azure.microsoft.com/services/cache)
- [Azure Cache for Redis 文档](/azure/azure-cache-for-redis/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
