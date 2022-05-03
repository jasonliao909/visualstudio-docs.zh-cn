---
title: 在 Visual Studio 中使用 GitHub 帐户
ms.date: 04/28/2022
ms.topic: how-to
description: 了解如何在 Visual Studio 中使用 GitHub 帐户。
ms.custom: devdivchpfy22
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: aaa65a77c4991dfae518e5e664f576d679c20b2c
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144547937"
---
# <a name="work-with-github-accounts-in-visual-studio"></a>在 Visual Studio 中使用 GitHub 帐户

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

如果你有公共 GitHub 或 GitHub Enterprise 帐户，可以将它添加到 Visual Studio 密钥链中。 添加帐户后，你就可以通过直接在 Visual Studio 中访问和创建 GitHub 存储库来利用平台集成。

## <a name="adding-public-github-accounts"></a>添加公共 GitHub 帐户

如果已使用 Microsoft 帐户、工作帐户或学校帐户登录到Visual Studio，则可以添加公共GitHub帐户。

1. 在 Visual Studio 环境的右上角，选择包含首字母的图标。 然后，选择“帐户设置...”来管理帐户。 还可以转到 **FileAccount** >  **设置...** 打开“帐户设置”对话框。

    :::image type="content" source="../ide/media/vs-2022/account-settings-1.png" alt-text="“帐户设置”窗口的屏幕截图。":::

1. 从 **“所有帐户”** 子菜单中，选择加号以添加帐户，然后选择 **GitHub**。

    :::image type="content" source="../ide/media/sign-in-add-github.png" alt-text="选择添加 GitHub 帐户":::

1. 此时，你被重定向到可以在其中使用 GitHub 凭据进行登录的浏览器。 登录后，你将在浏览器中看到“成功”窗口，然后可以返回到 Visual Studio。

    :::image type="content" source="../ide/media/github-success-signin.png" alt-text="浏览器中的“成功”窗口":::

1. 此时，这两个帐户同时出现在“所有帐户”子菜单下。

    :::image type="content" source="../ide/media/show-both-accounts.png" alt-text="两个帐户同时显示":::

如果尚未使用其他帐户登录到Visual Studio，请选择Visual Studio环境的右上角的 **“登录**”链接。 还可以转到 **FileAccount** >  **设置...** 打开“帐户设置”对话框。然后，按照上述说明添加GitHub帐户。

:::image type="content" source="../ide/media/vs-2022/signin-different-account.png" alt-text="未登录到 VS 2022":::

## <a name="adding-github-enterprise-managed-user-emu-accounts"></a>添加GitHub Enterprise托管用户 (EMU) 帐户

如果已使用 Microsoft 帐户、工作帐户或学校帐户登录到Visual Studio，则可以添加GitHub EMU 帐户。

1. 在 Visual Studio 环境的右上角，选择包含首字母的图标。 然后，选择“帐户设置...”来管理帐户。 还可以转到 **FileAccount** >  **设置...** 打开“帐户设置”对话框。

    :::image type="content" source="../ide/media/vs-2022/account-settings-1.png" alt-text="Enterprise托管用户的屏幕截图。":::

1. 从 **“所有帐户**”子菜单中，选择 **+**“**添加**”下拉列表以添加帐户，然后选择 **GitHub**。

    :::image type="content" source="../ide/media/sign-in-add-github.png" alt-text="显示如何选择和添加GitHub帐户的屏幕截图":::

1. 你将重定向到浏览器，可在其中使用 GitHub EMU 凭据登录。

> [!NOTE]
> 确保输入 GitHub EMU 帐户凭据， (用户名有下划线，后跟此页面上的公司名称) 。

:::image type="content" source="../ide/media/github-enterprise-managed-users-sign-in.png" alt-text="显示GitHub Enterprise托管用户帐户GitHub登录体验的屏幕截图":::

登录后，你将在浏览器中看到“成功”窗口，然后可以返回到 Visual Studio。

:::image type="content" source="../ide/media/github-success-signin.png" alt-text="显示浏览器中登录成功窗口的屏幕截图":::

## <a name="adding-github-enterprise-accounts"></a>添加 GitHub Enterprise 帐户

默认情况下，Visual Studio 只启用了公共 GitHub 帐户。

1. 若要启用 GitHub Enterprise 帐户，请依次转到“工具” > “选项”，然后搜索“帐户”选项。

    :::image type="content" source="../ide/media/vs-2022/add-github-enterprise-account.png" alt-text="GitHub帐户的屏幕截图。":::

1. 然后，选中“包括 GitHub Enterprise Server 帐户”复选框。 当你下次转到“帐户设置”并尝试添加 GitHub 帐户时，就会同时看到 GitHub 和 GitHub Enterprise 对应的选项。

    :::image type="content" source="../ide/media/github-enterprise-endpoint-signin.png" alt-text="使用 GitHub Enterprise 登录":::

1. 在输入 GitHub Enterprise 服务器地址后，选择“使用浏览器登录”。 在浏览器中，可以使用 GitHub Enterprise 凭据登录。

## <a name="see-also"></a>另请参阅
- [登录 Visual Studio](signing-in-to-visual-studio.md)
