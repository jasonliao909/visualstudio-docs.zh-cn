---
title: 使用 Azure 应用程序 Insights 添加连接的服务 |Microsoft Docs
description: 使用 Azure 应用程序 Insights 向应用添加Visual Studio连接服务
author: AngelosP
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: dc5bb07ef70ee5082fded77725205c1d29174ed4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602179"
---
# <a name="add-azure-application-insights-by-using-visual-studio-connected-services"></a>使用 Azure 应用程序 Insights 添加Visual Studio 连接的服务

使用 Visual Studio，可以使用 连接的服务 功能将以下任一项连接到 **Azure 应用程序 Insights：**

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

## <a name="connect-to-azure-application-insights-using-connected-services"></a>连接Azure 应用程序 Insights连接的服务

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器** 中，右键单击连接的服务节点，然后从上下文菜单中选择"**添加连接的服务"。**

1. 在 **"连接的服务"** 选项卡中，选择"服务依赖项 **"的"+"图标**。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在"**添加依赖项"页** 中，选择 **"Azure 应用程序 Insights"。**

    ![添加Azure 应用程序 Insights](./media/azure-app-insights-add-connected-service/azure-app-insights.png)

    如果还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/account/free)。

1. 在"**配置Azure 应用程序 Insights"** 屏幕中，选择现有Azure 应用程序 Insights组件，然后选择"下一 **步"。**

    如果需要创建新组件，请转到下一步。 否则，请跳到步骤 7。

    ![连接现有的应用程序Insights组件](./media/azure-app-insights-add-connected-service/created-app-insights.png)

1. 若要创建应用程序Insights组件：

   1. 选择 **屏幕底部的"Insights** 应用程序组件"。

   1. 填写"应用程序 **"Insights：创建新** 屏幕，然后选择"创建 **"。**

       ![新的 Azure 应用 Insights 组件](./media/azure-app-insights-add-connected-service/create-new-app-insights.png)

   1. 显示 **"配置Azure 应用程序 Insights"** 屏幕时，新组件将显示在列表中。 在列表中选择新组件，然后选择"下一 **步"。**

1. 输入检测密钥名称，或选择默认值，然后选择是希望连接字符串存储在本地机密文件中， [还是](/azure/key-vault)存储在 Azure Key Vault。

   ![指定连接字符串](./media/azure-app-insights-add-connected-service/connection-string.png)

1. " **更改摘要** "屏幕显示完成该过程后对项目所做的所有修改。 如果更改看起来正常，请选择"完成 **"。**

   ![更改摘要](./media/azure-app-insights-add-connected-service/summary-of-changes.png)

1. 连接显示在"连接 **"选项卡的** "服务依赖项 **"连接的服务** 下。

   ![服务依赖项](./media/azure-app-insights-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure Monitor产品页](https://azure.microsoft.com/services/monitor/)
- [Azure 应用 Insights文档](/azure/azure-monitor/app/app-insights-overview/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
