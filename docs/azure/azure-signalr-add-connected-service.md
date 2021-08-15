---
title: 使用 Azure SignalR 添加连接的服务 |Microsoft Docs
description: 使用门户将 Azure SignalR 添加到应用Visual Studio添加连接的服务
author: AngelosP
manager: jmartens
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 08/17/2020
ms.author: angelpe
monikerRange: '>= vs-2019'
ms.openlocfilehash: b97e97063c32e2cb97a1ef65c7d631f7a93200d774a6936f10dfdbd3627a6c96
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121312816"
---
# <a name="add-azure-signalr-by-using-visual-studio-connected-services"></a>使用 Azure SignalR 添加Visual Studio 连接的服务

使用 Visual Studio，可以使用以下任何一项连接到 Azure SignalR **服务**，连接的服务功能：

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
## <a name="prerequisites"></a>必备条件

- Visual Studio已安装 Azure 工作负载。
- 支持的类型之一的项目

## <a name="connect-to-azure-signalr-using-connected-services"></a>连接 Azure SignalR 连接的服务

1. 在 Visual Studio 中打开项目。

1. 在 **解决方案资源管理器** 中，右键单击连接的服务节点，然后从上下文菜单中选择"**添加连接的服务"。**

1. 在 **"连接的服务"** 选项卡中，选择"服务依赖项 **"的"+"图标**。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在"**添加依赖项"页** 中，选择 **"Azure SignalR 服务"。**

    ![添加Azure SignalR 服务](./media/azure-signalr-add-connected-service/add-signalr-service.png)

    如果还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/account/free)。

1. 在"**配置 Azure SignalR"** 屏幕中，选择现有的 Azure SignalR 组件，然后选择"下一 **步"。**

    如果需要创建新组件，请转到下一步。 否则，请跳到步骤 7。

    ![连接现有 Azure SignalR 组件](./media/azure-signalr-add-connected-service/created-signalr.png)

1. 若要创建 Azure SignalR 服务实例，请执行：

   1. 选择 **屏幕Azure SignalR 服务创建新的** 实例。

   1. 填写 **"Azure SignalR 服务：创建新屏幕**"，然后选择"创建 **"。**

       ![新Azure SignalR 服务实例](./media/azure-signalr-add-connected-service/create-new-signalr.png)

   1. 显示 **"配置Azure SignalR 服务"** 屏幕时，新实例将显示在列表中。 在列表中选择新实例，然后选择"下一 **步"。**

1. 输入连接字符串名称或选择默认值，然后选择是希望连接字符串存储在本地机密文件中， [还是](/azure/key-vault)存储在 Azure Key Vault。

   ![指定连接字符串](./media/azure-signalr-add-connected-service/connection-string.png)

1. " **更改摘要** "屏幕显示完成该过程后对项目所做的所有修改。 如果更改看起来正常，请选择"完成 **"。**

   ![更改摘要](./media/azure-signalr-add-connected-service/summary-of-changes.png)

1. 连接显示在"连接"选项卡的"服务 **依赖项****"连接的服务** 下。

   ![服务依赖项](./media/azure-signalr-add-connected-service/service-dependencies-after.png)

## <a name="see-also"></a>另请参阅

- [Azure SignalR 产品页](https://azure.microsoft.com/services/signalr-service/)
- [Azure SignalR 服务文档](/azure/azure-signalr)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
