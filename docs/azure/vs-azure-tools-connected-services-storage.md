---
title: 使用连接服务添加 Azure 存储 | Microsoft Docs
description: 使用 Visual Studio 连接服务将 Azure 存储服务依赖项添加到应用
author: ghogen
manager: jmartens
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: how-to
ms.date: 08/13/2020
ms.author: ghogen
ms.openlocfilehash: 995c4dc42de396dc9945aa553210c52e3c3cd661
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129969965"
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>使用 Visual Studio 连接服务添加 Azure 存储

在 Visual Studio 中，通过使用“连接服务”功能可将以下任何服务连接到 Azure 存储：

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

## <a name="connect-to-azure-storage-using-connected-services"></a>使用连接服务连接到 Azure Storage

::: moniker range="vs-2017"

1. 在 Visual Studio 中打开项目。

1. 在“解决方案资源管理器”中，右键单击“连接服务”节点，并在上下文菜单中选择“添加连接服务”。

    ![添加 Azure 连接服务](./media/vs-azure-tools-connected-services-storage/add-connected-service.png)

1. 在“连接服务”页面中，选择“Azure 存储的云存储”。

    ![添加 Azure 存储](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. 在“Azure 存储”对话框中，选择一个现有的存储帐户，并选择“添加”。

    若要要创建存储帐户，请转到下一步。 否则，请跳到步骤 6。

    ![将现有存储帐户添加到项目](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. 创建存储帐户：

   1. 选择对话框底部的“创建新存储帐户”。

   1. 填写“创建存储帐户”对话框，并选择“创建”。

       ![新的 Azure 存储帐户](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)

   1. 显示“Azure 存储”对话框时，新的存储帐户会显示在列表中。 在列表中选择新存储帐户，并选择“添加”。

1. 该存储连接服务会显示在项目的“服务引用”节点下。
:::moniker-end

:::moniker range=">=vs-2019"

1. 在 Visual Studio 中打开项目。

1. 在“解决方案资源管理器”中，右键单击“连接服务”节点，并在上下文菜单中选择“添加连接服务”。

    ![添加 Azure 连接服务](./media/vs-azure-tools-connected-services-storage/vs-2019/add-connected-service.png)

1. 在“连接服务”选项卡中，选择“服务依赖项”的 + 图标。

    ![添加服务依赖项](./media/vs-azure-tools-connected-services-storage/vs-2019/connected-services-tab.png)

1. 在“添加依赖项”页中，选择“Azure Storage”。

    ![添加 Azure 存储](./media/vs-azure-tools-connected-services-storage/vs-2019/add-azure-storage.png)

    如果你还没有登录，请登录到 Azure 帐户。 如果没有 Azure 帐户，可以注册[免费试用版](https://azure.microsoft.com/free/)。

1. 在“配置 Azure 存储”屏幕中，选择一个现有的存储帐户，并选择“下一步”。

    若要要创建存储帐户，请转到下一步。 否则，请跳到步骤 6。

    ![将现有存储帐户添加到项目](./media/vs-azure-tools-connected-services-storage/vs-2019/select-azure-storage-account.png)

1. 创建存储帐户：

   1. 选择对话框底部的“创建存储帐户”。

   1. 填写“Azure 存储: 新建”对话框，并选择“创建”。

       ![新的 Azure 存储帐户](./media/vs-azure-tools-connected-services-storage/vs-2019/create-storage-account.png)

   1. 显示“Azure 存储”对话框时，新的存储帐户会显示在列表中。 在列表中选择新存储帐户，并选择“下一步”。

1. 输入连接字符串名称，然后选择是要将连接字符串存储在本地机密文件中还是存储在 [Azure Key Vault](/azure/key-vault) 中。

   ![指定连接字符串](./media/vs-azure-tools-connected-services-storage/vs-2019/connection-string.png)

1. “更改摘要”屏幕显示了在完成该过程后将对项目进行的所有修改。 如果更改看起来正常，请选择“完成”。

   ![更改摘要](./media/vs-azure-tools-connected-services-storage/vs-2019/summary-of-changes.png)

1. 该存储连接服务会显示在项目的“服务引用”节点下。
:::moniker-end

## <a name="see-also"></a>另请参阅

- [Azure 存储论坛](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Azure 存储文档](/azure/storage/)
- [连接服务 (Visual Studio for Mac)](/visualstudio/mac/connected-services)
