---
title: 登录 Visual Studio for Mac
description: 如何登录 Visual Studio for Mac
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 04/26/2022
ms.assetid: E4CFD03C-03AF-48CA-B409-6DB1CA45E991
ms.custom: devdivchpfy22
ms.topic: how-to
ms.openlocfilehash: 3fa03846ad70321d98fe9597541ff69023efee5f
ms.sourcegitcommit: 1d5bf3876e092416b8735b3ba7788966b9502979
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2022
ms.locfileid: "144810288"
---
# <a name="sign-in-to-visual-studio-for-mac"></a>登录 Visual Studio for Mac

 [!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

登录到 Visual Studio for Mac 是[激活订阅](enable-subscription.md)的过程。 下载 Visual Studio for Mac 时，默认情况下，将始终获取社区版。 如果你有[Professional或Enterprise许可证](https://visualstudio.microsoft.com/vs/compare/)，则应首次登录以解锁任何其他功能。 此外，还可以获得以下功能：

* 访问 Visual Studio Dev Essentials 程序的权限 - 此程序包括免费软件产品/服务、培训、支持等。 请参阅 [Visual Studio Dev Essential](https://visualstudio.microsoft.com/dev-essentials/) 了解详细信息。

* 在 IDE 中自动连接到 Azure，而不会再次提示对同一帐户输入凭据。

首次启动Visual Studio for Mac时，系统会提示你使用 Microsoft 帐户登录。 使用已连接到要使用的许可证的 Microsoft 帐户。 如果没有 Microsoft 帐户，请参阅[如何实现注册帐户](https://support.microsoft.com/account-billing/how-to-create-a-new-microsoft-account-a84675c3-3e9e-17cf-2911-3d56b15c0aaf)。

登录后，可以访问与用户帐户以及链接到该帐户的所有帐户关联的所有服务。 无论在何处使用Visual Studio for Mac，帐户设置都随你一起漫游。 你可以为单个用户配置对特定 Visual Studio 实例的权限级别。

如果不立即登录，可使用评估副本 30 天。 30 天后，必须登录才能继续使用Visual Studio for Mac的副本。

## <a name="how-to-sign-in-to-visual-studio-for-mac"></a>如何登录 Visual Studio for Mac

> [!TIP]
> 登录到 Visual Studio for Mac 之前，请确保已连接到 Internet。 订阅只能联机激活。 如果未连接，请选择“稍后我将执行此操作”，并在连接后通过菜单登录。

若要在首次启动时登录到Visual Studio for Mac，请执行以下步骤：

::: moniker range="vsmac-2019"

1. 在登录窗口中选择 **“使用 Microsoft** 登录”按钮：

    ![Visual Studio for Mac 中的“帐户”对话框](media/ide-tour-2019-start-signin.png)

2. 输入 Microsoft 帐户凭据：

    ![“Microsoft 凭据”对话框](media/signing-in-image13.png)

3. 登录后，你将看到一个选择键盘快捷方式的选项。 选择要使用的 **选项并继续。** Visual Studio 2019 for Mac“启动”窗口将提醒你。 可在此处打开或创建新项目：

    ![登录成功](media/signing-in-image14.png)

或者，可以使用“Visual Studio”>“登录...” 菜单项随时登录和注销。

::: moniker-end

::: moniker range="vsmac-2022"

1. 在登录对话框中选择“ **使用 Microsoft 登录** ”按钮：

    :::image type="content" source="media/vsmac-2022/start-sign-in.png" alt-text="Visual Studio 2022 for Mac 中的登录帐户对话框的屏幕截图。":::

> [!NOTE]
> 如果选择 **“稍后我会执行此操作**”，则以后可以通过选择 **“登录”Visual Studio >登录来登录...** 从 **Visual Studio** 菜单中。

2. 输入 Microsoft 帐户凭据：

    :::image type="content" source="media/vsmac-2022/enter-sign-in-account-details.png" alt-text="在 Visual Studio 2022 for Mac 中输入登录帐户详细信息的屏幕截图。":::

3. 登录后，你将看到一个选择键盘快捷方式的选项。 选择要使用的 **选项并继续。** 然后，系统会提示使用 Visual Studio 2022 for Mac 开始窗口。 在这里，可以打开或创建新项目。

    :::image type="content" source="media/vsmac-2022/vsmac-launch.png" alt-text="在 Visual Studio for Mac 中打开或创建新项目窗口的屏幕截图 ":::

4. 从Visual Studio菜单中选择 **“Visual Studio >帐户...”** 以登录和注销或添加其他帐户。

    :::image type="content" source="media/vsmac-2022/account-window-after-sign-in.png" alt-text="Visual Studio 2022 for Mac 登录后帐户窗口的屏幕截图。":::

::: moniker-end

> [!TIP]
> 如果登录时遇到任何问题，请在“**无法登录”** 中尝试使用 **Web 浏览器** 选项登录？>**登录帐户** 窗口底部的其他选项下拉菜单。 如果 Mac 是使用条件访问的托管设备，则可能需要这样做。

## <a name="adding-multiple-user-accounts"></a>添加多个用户帐户

Visual Studio for Mac 支持向个性化帐户添加多个帐户。 这些帐户允许从任何添加的帐户访问资源，例如 Azure。

要添加其他用户帐户，请在 Visual Studio for Mac 中选择“Visual Studio”>“帐户...”菜单。 选择“ **添加...”** 按钮以输入其他帐户凭据。

::: moniker range="vsmac-2019"

![管理帐户](media/user-accounts-login.png)

::: moniker-end

::: moniker range="vsmac-2022"

:::image type="content" source="media/vsmac-2022/add-additional-accounts.png" alt-text="Visual Studio 2022 for Mac 中用于管理帐户的“帐户”窗口的屏幕截图":::

::: moniker-end

## <a name="view-or-change-your-profile-information"></a>查看或更改个人资料信息

1. 转到 Visual Studio >“帐户...”， 然后选择“个人资料”按钮。

2. 在浏览器窗口，选择“编辑配置文件”并更改所需的设置。

3. 完成后，选择“保存更改”。

## <a name="see-also"></a>请参阅

- [启用订阅](enable-subscription.md)
- [登录 Visual Studio (Windows)](/visualstudio/ide/signing-in-to-visual-studio)
- [使用多个用户帐户（Windows 上的 Visual Studio）](/visualstudio/ide/work-with-multiple-user-accounts)
