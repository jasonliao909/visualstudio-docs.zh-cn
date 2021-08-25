---
title: 登录
description: 登录 Visual Studio 以延长 Visual Studio 试用期、解锁 Visual Studio 等等
ms.custom: contperf-fy21q1
ms.date: 09/11/2020
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 8d674a46ec68810df8575f963bccf9b2ed70f574
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122040939"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>在 Windows 上登录到 Visual Studio 

虽然无需登录，但登录有很多好处。 在本文中，你将了解[如何登录](#how-to-sign-in)、如何[更新个人资料](#update-your-profile)，以及 Visual Studio 体验的好处。 

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[登录到 Visual Studio for Mac](/visualstudio/mac/signing-in)。

::: moniker range="vs-2017"

> [!WARNING]
> 若要使用为条件访问配置的资源，请升级到 Visual Studio 2019 Update 16.6 或更高版本。 有关详细信息，请参阅[如何将 Visual Studio 与需要多重身份验证的帐户一起使用](work-with-multi-factor-authentication.md)。
> 使用 Visual Studio 2017 访问为条件访问配置的资源时，可能会触发降级身份验证体验，进而在同一 Visual Studio 会话中多次提示重新进行身份验证。 
> 
::: moniker-end

以下是登录后可体验的内容及可执行的操作的完整列表：

|好处|描述|
|---|---|
|延长 Visual Studio 试用期|可将 Visual Studio Professional 或 Visual Studio Enterprise 的使用期延长 90 天，而不是仅限于 30 天的试用期。 <br/>请参阅[扩展试用版或更新许可证](../ide/how-to-unlock-visual-studio.md)。|
|解锁 Visual Studio（Visual Studio 订阅或 Azure DevOps 组织）|如果使用与 Microsoft Visual Studio 订阅或 Azure DevOps 组织相关联的帐户，解锁 Visual Studio。<br/>请参阅[扩展试用版或更新许可证](../ide/how-to-unlock-visual-studio.md)。|
|同步 Visual Studio 设置|登录到任何设备上的 Visual Studio 时，将立即应用自定义设置（例如键绑定、窗口布局和颜色主题）。 <br/>请参阅 [Visual Studio 中的同步设置](../ide/synchronized-settings-in-visual-studio.md)。|
|自动连接到服务|在 IDE 中连接到服务（如 Azure 和 Azure DevOps Services），而不会再次提示对同一帐户输入凭据。|
|继续使用 Visual Studio Community 版本|如果安装 Community 版时提示你提供许可证，请登录 IDE 以继续免费使用 Visual Studio Community。 |
|获取“Visual Studio Dev Essentials”|该计划包括免费软件产品/服务、培训、支持等。 <br/>请参阅 [Visual Studio Dev Essentials](https://visualstudio.microsoft.com/dev-essentials/)。|


## <a name="how-to-sign-in"></a>登录方法 

首次打开 Visual Studio 时，系统将要求登录并提供一些基本注册信息。

![登录提示](../ide/media/vs2019_signinpopup.png)

1. 选择最能够满足你需求的 Microsoft 帐户或工作/学校帐户。 如果你没有此类帐户，可以单击“登录”按钮下的链接，免费创建一个 Microsoft 帐户。 如果遇到问题，请参阅[如何注册 Microsoft 帐户？](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)

2. 选择要在 Visual Studio 中使用的 UI 设置和颜色主题。 Visual Studio 会记住这些设置并将其同步到登录到的所有 Visual Studio 环境。 有关已同步的设置列表，请参阅[已同步的设置](../ide/synchronized-settings-in-visual-studio.md)。 以后可以打开 Visual Studio 中的“工具” > “选项”菜单来更改设置 。
   提供设置后，Visual Studio 将启动，然后你就会进行登录并准备好开始操作。 
   
1. 若要验证你是否已登录，请在 Visual Studio 环境的右上角查找名称。

![VS2019 中当前已登录的用户](../ide/media/vs2019_username.png)

如果你选择在首次打开 Visual Studio 时不登录，可以在以后轻松登录。 查找 Visual Studio 环境的右上角中的“登录”链接。

![不是已登录用户](../ide/media/vs2019_usernotsignedin.png)

除非注销，否则在启动 Visual Studio 时会自动登录，并自动应用于对同步设置所做的所有更改。 若要注销，请单击 Visual Studio 环境右上角显示个人资料名称的图标，然后依次选择“帐户设置”命令和“注销”链接 。 若要再次登录，请选择 Visual Studio 环境的右上角中的 **“登录”** 命令。

## <a name="update-your-profile"></a>更新配置文件

1. 转到“文件” > “帐户设置”，然后选择“管理 Visual Studio 配置文件”链接  。

1. 在浏览器窗口，选择“编辑配置文件”并更改所需的设置。

1. 完成后，选择“保存更改”。

## <a name="troubleshooting"></a>疑难解答

请参阅[订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)页面以获取帮助。
