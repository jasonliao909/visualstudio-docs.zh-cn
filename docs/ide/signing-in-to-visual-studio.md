---
title: 登录
description: 登录 Visual Studio 以延长 Visual Studio 试用期、解锁 Visual Studio 等等
ms.custom: contperf-fy21q1
ms.date: 12/10/2021
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 2c5198d2b99f2f808e3c42c2f35bfcfd9188941a
ms.sourcegitcommit: ebd651e00fe3bae5914c211c4828219bf7d1fc70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2022
ms.locfileid: "137798595"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>在 Windows 上登录到 Visual Studio 

本文内容：
+ [帐户登录的好处](#benefits)
+ 如何使用帐户[登录](#sign-in)
+ 如何 [更新配置文件](#update-your-profile)

::: moniker range="vs-2017"

> [!WARNING]
> 若要使用配置为条件访问或多重身份验证的资源，需要 Visual Studio 2019 更新16.6 或更高版本。 早期版本可能会触发降级的身份验证体验，并在同一 Visual Studio 会话中多次重新进行身份验证。 

::: moniker-end

<a name="benefits"></a>
## <a name="benefits-why-sign-in"></a>优势：为何登录？ 

虽然无需登录，但登录有很多好处。   

|好处|描述|
|---|---|
|[延长 Visual Studio 试用期](../ide/how-to-unlock-visual-studio.md)|可将 Visual Studio Professional 或 Visual Studio Enterprise 的使用期延长 90 天，而不是仅限于 30 天的试用期。|
|[解锁 Visual Studio](../ide/how-to-unlock-visual-studio.md)|如果使用与[Visual Studio 订阅](/visualstudio/subscriptions/using-the-subscriber-portal)或 Azure DevOps 组织关联的帐户，则解除 Visual Studio 锁定。|
|[同步](../ide/synchronized-settings-in-visual-studio.md) 设置|登录到任何设备上的 Visual Studio 时，将立即应用自定义设置（例如键绑定、窗口布局和颜色主题）。|
|自动连接到 Azure 服务|在 IDE 中连接到服务（如 Azure 和 Azure DevOps Services），而不会再次提示对同一帐户输入凭据。|
|继续使用我们的 Community 版本|如果安装提示你提供许可证，请登录到 IDE 以继续 **免费** 使用 Visual Studio Community。 |
|[获取“Visual Studio Dev Essentials”](https://visualstudio.microsoft.com/dev-essentials/)|此计划包括免费软件、培训、支持等。|

<a name="sign-in"></a>
## <a name="sign-in-to-account"></a>登录帐户

::: moniker range="<=vs-2019"

1. 启动 Visual Studio。 首次打开 Visual Studio 时，系统将要求登录并提供一些基本注册信息。

   ![登录提示](../ide/media/vs2019_signinpopup.png)
   
   > [!NOTE]
   > 如果你选择在首次打开 Visual Studio 时不登录，可以在以后轻松登录。 查找 Visual Studio 环境的右上角中的“登录”链接。

::: moniker-end

::: moniker range="vs-2022"

1. 启动 Visual Studio。  首次打开 Visual Studio 时，系统将要求登录并提供一些基本注册信息。

   ![登录提示](../ide/media/vs-2022/visual-studio-sign-in-pop-up.png)

::: moniker-end

2. 选择 Microsoft 帐户或工作或学校帐户。  如果没有，请选择 "**登录**" 按钮附近的链接，[免费创建一个 Microsoft 帐户](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)。 

3. 选择首选的颜色主题和其他 UI 设置。  Visual Studio 会[记住这些设置并](../ide/synchronized-settings-in-visual-studio.md)将其同步到登录到的所有 Visual Studio 环境中。 以后可以打开 Visual Studio 中的“工具” > “选项”菜单来更改设置 。

   你可以看到你已成功登录到 Visual Studio 环境的右上角。   除非注销，否则在启动 Visual Studio 时会自动登录，并自动应用于对同步设置所做的所有更改。

::: moniker range="<=vs-2019"

   ![VS2019 中当前已登录的用户](../ide/media/vs2019_username.png)

::: moniker-end

::: moniker range="vs-2022"

   ![VS2019 中当前已登录的用户](../ide/media/vs-2022/visual-studio-sign-in.png)

::: moniker-end


## <a name="sign-out-of-account"></a>注销帐户

1. 在 Visual Studio 环境的右上角单击带有配置文件名称的图标
2. 选择 " **帐户设置** " 命令。
3. 选择 " **注销** " 链接。 

## <a name="update-your-profile"></a>更新配置文件

1. 转到“文件” > “帐户设置”，然后选择“管理 Visual Studio 配置文件”链接  。
1. 在浏览器窗口，选择“编辑配置文件”并更改所需的设置。
1. 完成后，选择“保存更改”。

## <a name="see-also"></a>请参阅

- 故障排除： [订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)
- [Visual Studio 2022 版比较](https://visualstudio.microsoft.com/vs/compare/)
