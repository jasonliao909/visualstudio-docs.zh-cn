---
title: 登录
description: 了解如何登录Visual Studio、如何登录以及如何添加和切换用户帐户。
ms.custom: contperf-fy21q1
ms.date: 04/28/2022
ms.topic: how-to
ms.assetid: b9531c25-e4cf-43ae-b331-a9f31a8cd171
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 9ca4d29e280524338ef37822c672598ccd1b088c
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144547950"
---
# <a name="sign-in-to-visual-studio-on-windows"></a>在 Windows 上登录到 Visual Studio 

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

本文内容：
+ [帐户登录的好处](#benefits)
+ 如何使用帐户[登录](#sign-in)
+ 如何 [添加和切换](#add-and-switch) 用户帐户
+ 如何 [访问](#access) 多个用户帐户
+ 如何 [注销](#sign-out-of-account) 帐户
+ 如何 [更新](#update-your-account-profile) 个人资料

::: moniker range="vs-2017"

> [!WARNING]
> 若要使用配置为条件访问或多重身份验证的资源，需要Visual Studio 2019 Update 16.6 或更高版本。 早期版本可能会触发降级的身份验证体验，在同一个Visual Studio会话中多次提示重新进行身份验证。 

::: moniker-end

<a name="benefits"></a>
## <a name="benefits-why-sign-in"></a>优点：为什么登录？ 

虽然无需登录，但登录有很多好处。   

|好处|描述|
|---|---|
|[延长Visual Studio试用期](../ide/how-to-unlock-visual-studio.md)|可将 Visual Studio Professional 或 Visual Studio Enterprise 的使用期延长 90 天，而不是仅限于 30 天的试用期。|
|[解锁 Visual Studio](../ide/how-to-unlock-visual-studio.md)|如果使用与[Visual Studio订阅或Azure DevOps](/visualstudio/subscriptions/using-the-subscriber-portal)组织关联的帐户，请解锁Visual Studio。|
|[同步](../ide/synchronized-settings-in-visual-studio.md) 设置|登录到任何设备上的 Visual Studio 时，将立即应用自定义设置（例如键绑定、窗口布局和颜色主题）。|
|自动连接到 Azure 服务|在 IDE 中连接到服务（如 Azure 和 Azure DevOps Services），而不会再次提示对同一帐户输入凭据。|
|继续使用我们的 Community 版本，而不会中断|如果安装提示你定期登录，请登录到 IDE 以继续使用Visual Studio Community而不中断。|
|[获取“Visual Studio Dev Essentials”](https://visualstudio.microsoft.com/dev-essentials/)|此计划包括免费软件、培训、支持等。|

<a name="sign-in"></a>
## <a name="sign-in-with-a-microsoft-account-or-an-organizational-account"></a>使用 Microsoft 帐户或组织帐户登录

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

2. 选择 Microsoft 帐户或工作或学校帐户。  如果没有帐户，请通过选择 **“登录**”按钮附近的链接 [免费创建 Microsoft 帐户](https://support.microsoft.com/help/4026324/microsoft-account-how-to-create)。 

3. 选择首选的颜色主题和其他 UI 设置。  Visual Studio[记住这些设置，并在](../ide/synchronized-settings-in-visual-studio.md)已登录的所有Visual Studio环境中同步这些设置。 以后可以打开 Visual Studio 中的“工具” > “选项”菜单来更改设置 。

   可以看到已成功登录到Visual Studio环境的右上角。   除非注销，否则在启动 Visual Studio 时会自动登录，并自动应用于对同步设置所做的所有更改。

::: moniker range="<=vs-2019"

   ![VS2019 中当前已登录的用户](../ide/media/vs2019_username.png)

::: moniker-end

::: moniker range="vs-2022"

   ![VS2019 中当前已登录的用户](../ide/media/vs-2022/visual-studio-sign-in.png)

::: moniker-end

<a name="add-and-switch"></a>
## <a name="add-and-switch-user-accounts"></a>添加和切换用户帐户

如果有多个 Microsoft 帐户和/或单位或学校帐户，可将它们全部添加到 Visual Studio，以便可从任何帐户访问资源，而无需单独登录到这些帐户。

将多个帐户添加到一台计算机上之后，如果你在另一台计算机上登录到 Visual Studio，则该组帐户会随你一起漫游。

> [!NOTE]
> 尽管帐户名可漫游，但凭据却不能。 第一次尝试在新的计算机上使用其资源时，将提示你输入这些其他帐户的凭据。

::: moniker range=">=vs-2019"

### <a name="add-an-additional-account-to-visual-studio"></a>向 Visual Studio 添加另一个帐户

若要将其他帐户添加到 Visual Studio：

1. 选择 **文件** > **帐户设置**。

1. 从 **“所有帐户**”中，使用 **+** “ **添加** ”下拉列表选择帐户。

1. 在“登录到你的帐户”页面上，选择该帐户或选择“使用另一个帐户”   。 按照提示输入新的帐户凭据。

（可选）现在可以转到“服务器资源管理器”，并查看与刚添加的帐户相关联的 Azure 服务  。 在“服务器资源管理器”中，右键单击“Azure”节点并选择“管理和筛选订阅”    。 通过单击当前帐户旁的下拉箭头选择新的帐户，然后选择想要在“服务器资源管理器”中显示的订阅  。 应可以看到与指定订阅关联的所有服务。 即使当前未使用第二个帐户登录到 Visual Studio，也可登录到该帐户的服务和资源。 Project  > **Add Connected Service** 也是如此。
::: moniker-end

::: moniker range="vs-2017"
### <a name="add-an-additional-account-to-visual-studio"></a>向 Visual Studio 添加另一个帐户

若要将其他帐户添加到 Visual Studio：

1. 选择 **文件** > **帐户设置**。

1. 在“所有帐户”下，选择“添加帐户”   。

1. 在“登录到你的帐户”页面上，选择该帐户或选择“使用另一个帐户”   。 按照提示输入新的帐户凭据。

（可选）现在可以转到“服务器资源管理器”，并查看与刚添加的帐户相关联的 Azure 服务  。 在“服务器资源管理器”中，右键单击“Azure”节点并选择“管理和筛选订阅”    。 通过单击当前帐户旁的下拉箭头选择新的帐户，然后选择想要在“服务器资源管理器”中显示的订阅  。 应可以看到与指定订阅关联的所有服务。 即使当前未使用第二个帐户登录到 Visual Studio，也可登录到该帐户的服务和资源。 “项目”   > “添加连接的服务”  和“团队”   > “连接到 Team Foundation Server”  也是如此。

### <a name="add-an-account-using-device-code-flow"></a>使用设备代码流添加帐户

在某些情况下，无法以常规方式登录或添加帐户。 如果 Internet Explorer 因某种原因被阻止，或网络设置了防火墙，则可能发生这种情况。 要解决此问题，可以启用“设备代码流”来添加帐户或重新验证帐户  。 借助设备代码流，可使用另一种浏览器或在另一个物理或虚拟 (VM) 机&mdash;上登录。

使用设备代码流登录：

1. 打开“工具” > “选项” > “环境”下的 [“帐户”](reference/accounts-environment-options-dialog-box.md)页面，然后选择“在添加或重新验证帐户时启用设备代码流”。 选择“确定”关闭选项页  。

1. 选择 **“文件** > **帐户”设置** 以打开帐户管理页。

1. 在“所有帐户”下，选择“添加帐户”   。

   会出现一个对话框，其中显示了要粘贴到 web 浏览器中的 URL 和代码。

   ![设备代码流 URL 和代码](media/work-with-multiple-user-accounts/device-login-code.png)

1. 按“Ctrl+C”复制对话框文本，然后选择“确定”关闭对话框。 将复制的文本粘贴到文本编辑器（如记事本）中。 这使得在下一步中复制代码更加容易。

1. 导航到机器或 web 浏览器上用于登录到 Visual Studio 的设备登录 URL，然后将复制的代码粘贴或输入到“代码”框中  。

   “Visual Studio”应用名称应会显示在页面的更下方  。

1. 在“Visual Studio”下，选择“继续”   。

   ![“设备登录”页面的屏幕截图，其中显示了“继续”选项。](media/work-with-multiple-user-accounts/device-login-page.png)

1. 按照提示输入帐户凭据。

   随即出现一个页面，提示已在设备上登录 Visual Studio，可以关闭浏览器窗口。

   ![通过浏览器登录 visual Studio 这一操作已完成](media/work-with-multiple-user-accounts/sign-in-browser-complete.png)

1. 返回 Visual Studio 中的帐户管理页面，其中的“所有帐户”下列出了新添加的帐户  。 选择“关闭”  。

::: moniker-end

::: moniker range=">=vs-2019"

### <a name="add-a-github-account-to-visual-studio"></a>向 Visual Studio 添加 GitHub 帐户

自版本 16.8 起，可以将 GitHub 和 GitHub Enterprise 帐户都添加到密钥链中。 你可以添加并使用这些帐户，就像使用 Microsoft 帐户一样；也就是说，你将能够更轻松地跨 Visual Studio 访问 GitHub 资源。

有关详细说明，请参阅[在 Visual Studio 中使用 GitHub 帐户](work-with-github-accounts.md)。

### <a name="add-a-multi-factor-authentication-mfa-enabled-account-to-visual-studio"></a>将启用了 MFA) 的多重身份验证 (帐户添加到Visual Studio

在 Visual Studio 2019 16.6 版本中，我们添加了新的功能，该功能简化了用户对受 CA 策略（如 MFA）保护资源的访问方式。 要使用此增强工作流，需要选择使用系统的默认 Web 浏览器作为添加并重新验证 Visual Studio 帐户的机制。

有关详细说明，请参阅 [使用需要多重身份验证的帐户 (MFA) ](work-with-multi-factor-authentication.md)

::: moniker-end

<a name="access"></a>
## <a name="access-multiple-accounts-associated-with-the-visual-studio-sign-in-account"></a>访问与Visual Studio登录帐户关联的多个帐户

使用 Microsoft 或组织帐户登录Visual Studio后，可以在 **“添加连接服务**”对话框、**服务器资源管理器** 和 **团队资源管理器** 等位置查看帐户访问的资源。

Azure、Application Insights、Azure DevOps 和 Microsoft 365 服务都支持简化的登录体验。

### <a name="access-your-azure-account-in-server-explorer"></a>在服务器资源管理器中访问你的 Azure 帐户

若要打开服务器资源管理器，请选择“查看” > “服务器资源管理器”（或者，如果使用的是“常规”[环境设置](../ide/environment-settings.md)，请按 Ctrl+Alt+S）。 展开“Azure”节点，注意它包含 Azure 帐户中可用的资源，该资源与用于登录 Visual Studio 的帐户相关联  。 它看上去类似于下图：

::: moniker range="<=vs-2019"

![展开了 Azure 节点的服务器资源管理器](../ide/media/work-with-multiple-user-accounts/server-explorer.png)

::: moniker-end

::: moniker range="vs-2022"

![展开了 Azure 节点的服务器资源管理器](../ide/media/vs-2022/server-explorer.png)

::: moniker-end

在任何特定设备上首次使用 Visual Studio 时，对话框都将只显示在登录的账户下注册的订阅。 通过右键单击“Azure”节点、选择“管理和筛选订阅”并从帐户选取器控件添加帐户，可以直接从“服务器资源管理器”访问任何其他帐户的资源    。 如果需要，可以通过单击向下箭头，从帐户列表中选择另一个帐户。 选择帐户之后，可以自定义帐户下的哪些订阅在“服务器资源管理器”中显示  。

![“管理 Azure 订阅”对话框](../ide/media/vs2015_manage_subs.png)

下次打开“服务器资源管理器”时，将显示所选订阅的资源  。

### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>通过“添加连接的服务”对话框，访问你的 Azure 帐户

1. 打开一个现有项目，或创建一个新项目。

1. 选择“解决方案资源管理器”中的项目节点，然后右键单击并选择“添加” > “连接的服务”。

   此时会显示 **“连接服务**”窗口，并显示与Visual Studio个性化帐户关联的 Azure 帐户中的服务列表。 无需单独登录 Azure。 但是，第一次尝试从另一计算机访问其资源时，你需要登录到其他帐户。

### <a name="access-azure-active-directory-in-a-web-project"></a>在 Web 项目中访问 Azure Active Directory

Azure Active Directory (Azure AD) 支持最终用户单一登录 ASP.NET Web API 服务中的 MVC Web 应用或 AD 身份验证。 域身份验证与单个用户帐户身份验证不同。 有权访问 Active Directory 域的用户可以使用其现有的Azure AD帐户连接到 Web 应用程序。 Microsoft 365 应用还可以使用域身份验证。

::: moniker range="vs-2017"

要了解此操作，请创建一个新的“ASP.NET Core Web 应用程序”项目  。 在“新建 ASP.NET Core Web 应用程序”对话框中，选择“Web 应用程序”模板，然后选择“更改身份验证”    。

随即显示“更改身份验证”对话框，你可以在该对话框中选择要在应用程序中使用的身份验证类型  。

![适用于 ASP.NET 的更改身份验证对话框](../ide/media/vs2015_change_authentication.png)

有关 ASP.NET 中不同类型的身份验证的详细信息，请参阅[在 Visual Studio 中创建 ASP.NET web 项目](/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#authentication-methods)。

### <a name="access-your-azure-devops-organization"></a>访问 Azure DevOps 组织

在主菜单中，选择“团队” > “管理连接”以打开“团队资源管理器 - 连接”窗口。 选择“管理连接” > “连接到项目”。 在“连接到项目”对话框中，从列表中选择一个项目（或选择“添加 TFS 服务器”并输入服务器的 URL）   。 选择 URL 后，无需重新输入凭据即可登录。

有关详细信息，请参阅[连接到团队资源管理器中的项目](connect-team-project.md)。

::: moniker-end

::: moniker range="vs-2019"

要了解此操作，请创建一个新的“ASP.NET Core Web 应用”项目。 在 **“其他信息**”页上，从 **“目标框架**”下拉列表中选择 **.NET Core 3.1 () 长期支持**，然后从 **“身份验证类型**”下拉列表中选择身份验证类型。

::: moniker-end

::: moniker range=">=vs-2022"

要了解此操作，请创建一个新的“ASP.NET Core Web 应用”项目。 在 **“其他信息**”页上，从 **“目标框架**”下拉列表中选择 **.NET Core 6 (长期支持)**，然后从 **“身份验证类型**”下拉列表中选择身份验证类型。

::: moniker-end

## <a name="sign-out-of-account"></a>注销帐户

1. 在Visual Studio环境的右上角选择配置文件名称的图标。
1. 选择 **“帐户设置”。。**
1. 选择“注销”。

## <a name="update-your-account-profile"></a>更新帐户配置文件

1. 转到 **“文件>帐户设置...”**，然后选择 **“管理Visual Studio配置文件**”链接。
1. 在浏览器窗口中，选择 **“编辑配置文件** ”并更改所需的设置。
1. 完成操作后，选择“保存更改”。

## <a name="see-also"></a>另请参阅

- 故障排除： [订阅支持](https://visualstudio.microsoft.com/subscriptions/support/)
- [比较 Visual Studio 2022 版本](https://visualstudio.microsoft.com/vs/compare/)
