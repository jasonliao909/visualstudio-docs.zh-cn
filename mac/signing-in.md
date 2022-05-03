---
title: 登录 Visual Studio for Mac
description: 如何登录 Visual Studio for Mac
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 03/03/2022
ms.assetid: E4CFD03C-03AF-48CA-B409-6DB1CA45E991
ms.custom: devdivchpfy22
ms.topic: how-to
ms.openlocfilehash: 6dea97a22926f1d8b344d98b156d2882c3962fb9
ms.sourcegitcommit: fcf47a9c356df7e9636bcab92186923e5c9b8892
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2022
ms.locfileid: "144507253"
---
# <a name="sign-in-to-visual-studio-for-mac"></a>登录 Visual Studio for Mac

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

登录到 Visual Studio for Mac 是[激活订阅](enable-subscription.md)的过程。 下载 Visual Studio for Mac 时，默认情况下，将始终获取社区版。 如果你有[Professional或Enterprise许可证](https://visualstudio.microsoft.com/vs/compare/)，则应首次登录以解锁任何其他功能。 此外，还可以获得以下功能：

* 访问 Visual Studio Dev Essentials 程序的权限 - 此程序包括免费软件产品/服务、培训、支持等。 请参阅 [Visual Studio Dev Essential](https://visualstudio.microsoft.com/dev-essentials/) 了解详细信息。

* 在 IDE 中自动连接到 Azure，而不会再次提示对同一帐户输入凭据。

首次启动Visual Studio for Mac时，系统会提示你使用 Microsoft 帐户登录。 使用已连接到要使用的许可证的 Microsoft 帐户。 如果没有 Microsoft 帐户，请参阅[如何实现注册帐户](https://support.microsoft.com/account-billing/how-to-create-a-new-microsoft-account-a84675c3-3e9e-17cf-2911-3d56b15c0aaf)。

如果不立即登录，可使用评估副本 30 天。 30 天后，必须登录才能继续使用Visual Studio for Mac的副本。

## <a name="how-to-sign-in-to-visual-studio-for-mac"></a>如何登录 Visual Studio for Mac

> [!TIP]
> 登录到 Visual Studio for Mac 之前，请确保已连接到 Internet。 > 订阅只能联机激活。 如果未连接，请选择“稍后再执行此操作”，并在连接后通过菜单登录。

要在第一次启动时登录 Visual Studio for Mac，请执行以下步骤：

1. 在登录窗口中选择“ **使用 Microsoft 登录** ”按钮：

    ![Visual Studio for Mac 中的“帐户”对话框](media/ide-tour-2019-start-signin.png)

2. 输入 Microsoft 凭据：

    ![“Microsoft 凭据”对话框](media/signing-in-image13.png)

4. 登录后，你将看到一个选择键盘快捷方式的选项。 选择要使用的选项，然后继续操作。 Visual Studio 2019 for Mac“启动”窗口将提醒你。 可在此处打开或创建新项目：

    ![登录成功](media/signing-in-image14.png)

或者，可以使用“Visual Studio”>“登录...” 菜单项随时登录和注销。

> [!TIP]
> 如果在登录时遇到任何问题，请尝试使用“登录帐户”窗口底部的“无法登录?”下拉菜单中的“使用 Web 浏览器登录”选项。 如果 Mac 是使用条件访问的托管设备，则可能需要这样做。

## <a name="adding-multiple-user-accounts"></a>添加多个用户帐户

Visual Studio for Mac 支持向个性化帐户添加多个帐户。 这些帐户允许从任何添加的帐户访问资源，例如 Azure。

要添加其他用户帐户，请在 Visual Studio for Mac 中选择“Visual Studio”>“帐户...”菜单。 选择 **“添加...”** 按钮以输入其他帐户凭据。

![管理帐户](media/user-accounts-login.png)

## <a name="view-or-change-your-profile-information"></a>查看或更改个人资料信息

1. 转到 Visual Studio >“帐户...”， 然后选择“个人资料”按钮。

2. 在浏览器窗口，选择“编辑配置文件”并更改所需的设置。

3. 完成后，选择“保存更改”。

## <a name="see-also"></a>请参阅

- [登录 Visual Studio (Windows)](/visualstudio/ide/signing-in-to-visual-studio)
- [使用多个用户帐户（Windows 上的 Visual Studio）](/visualstudio/ide/work-with-multiple-user-accounts)
