---
title: Visual Studio 登录的多重身份验证
titleSuffix: ''
ms.date: 04/28/2022
ms.custom: SEO-VS-2022
ms.topic: how-to
description: 了解如何将Visual Studio用于需要多重身份验证的帐户 (MFA) 。
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
monikerRange: '>=vs-2019'
ms.openlocfilehash: 469621a16e7fe63704e88c1bad8e21d489abd85a
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144547912"
---
# <a name="sign-in-to-visual-studio-with-accounts-that-require-multi-factor-authentication-mfa"></a>使用需要多重身份验证 (MFA) 的帐户登录Visual Studio

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

本文介绍如何将Visual Studio用于需要多重身份验证的帐户 (MFA) 。

## <a name="why-enable-mfa-policies"></a>为什么启用 MFA 策略？

在与外部来宾用户协作时，最好使用条件访问 (CA) 策略（例如多重身份验证 (MFA)）来保护你的应用和数据 。  

启用后，来宾用户不仅需要用户名和密码来访问你的资源，而且还必须满足其他安全要求。 可在租户、应用或个人来宾用户级别上强制实施 MFA 策略，操作方式与为你自己的组织成员启用这些策略的方式相同。 

## <a name="how-is-the-visual-studio-experience-affected-by-mfa-policies"></a>MFA 策略会对 Visual Studio 体验带来什么影响？
与启用了 CA 策略（例如 MFA）并与两个或多个租户相关联的帐户一起使用时，Visual Studio 16.6 之前的版本可能会降低身份验证体验。

这些问题可能会导致你的 Visual Studio 实例每天多次提示重新验证。 即使在同一Visual Studio会话过程中，你可能需要重新输入以前经过身份验证的租户的凭据。

## <a name="using-visual-studio-with-mfa-policies"></a>搭配使用 Visual Studio 与 MFA 策略
在 Visual Studio 2019 16.6 版本中，我们添加了新的功能，该功能简化了用户对受 CA 策略（如 MFA）保护资源的访问方式。 要使用此增强工作流，需要选择使用系统的默认 Web 浏览器作为添加并重新验证 Visual Studio 帐户的机制。  

> [!WARNING]
> 如果未使用此工作流，则在添加或重新验证 Visual Studio 帐户时，可能会触发降级的体验，导致多次额外的身份验证提示。 

### <a name="enabling-system-web-browser"></a>启用系统 Web 浏览器

> [!NOTE] 
> 为了获得最佳体验，建议在继续此工作流之前清除系统的默认 Web 浏览器数据。 此外，如果 Windows 10 设置中的“访问工作或学校”下有工作或学校帐户，请验证它们是否已正确通过身份验证。

要启用此工作流，请转到 Visual Studio 的“选项”对话框（“工具”>“选项…”），选择“帐户”选项卡，然后在“使用以下方式添加并重新验证帐户:”下拉列表中选取“系统 Web 浏览器”   。 

:::image type="content" source="media/vs-2022/select-system-web-browser.png" alt-text="从菜单中选择系统 Web 浏览器。":::

### <a name="sign-into-additional-accounts-with-mfapolicies"></a>使用 MFA 策略登录其他帐户 
启用系统 Web 浏览器工作流后，可以通过“帐户设置”对话框（“文件”>“帐户设置…”）按常规方式登录或向 Visual Studio 添加帐户。   
</br>
:::image type="content" source="media/vs-2022/add-personalization-account.png" alt-text="向 Visual Studio 添加新的个性化帐户。" border="false":::

此操作将打开系统的默认 Web 浏览器，要求你登录帐户，并验证任何所需的 MFA 策略。

在登录过程中，可能会收到其他提示，要求你保持登录状态。 在第二次使用帐户登录时，可能会显示此提示。 为了最大限度地减少重新输入凭据的需要，建议选择“是”，因为这可确保在浏览器会话中保留凭据。

:::image type="content" source="media/vs-2022/keep-me-signed-in.png" alt-text="保持登录状态？":::

根据开发活动和资源配置，你仍可能会提示你在会话期间重新输入凭据。 当你添加新资源或尝试访问资源时，如果之前未满足其 CA/MFA 授权要求，可能会发生这种情况。

## <a name="reauthenticating-an-account"></a>重新验证帐户
如果帐户出现问题，Visual Studio可能会要求你重新输入帐户凭据。  

:::image type="content" source="media/vs-2022/reauthenticate-account.png" alt-text="重新验证 Visual Studio 帐户。":::

单击 **“重新输入凭据** ”将打开系统的默认 Web 浏览器，并尝试自动刷新凭据。 如果失败，系统将要求登录你的帐户并验证任何所需的 CA/MFA 策略。

> [!NOTE] 
> 为了获得最佳体验，请保持浏览器打开，直到为资源验证了所有 CA/MFA 策略。 关闭浏览器可能会导致以前生成的 MFA 状态丢失，并且可能会提示其他授权提示。

### <a name="troubleshooting-sign-in-issues"></a>排查登录问题
如果遇到 CA/MFA 问题并且/或者即使使用系统 Web 浏览器也无法登录，请尝试以下步骤来解决此问题：

1. [在 Visual Studio 中注销](signing-in-to-visual-studio.md#sign-out-of-account)帐户。
1. 选择 **ToolsOptionsAccounts** >  >  >在所有 **Azure Active Directory 中取消选中“身份验证**”。
1. 再次登录。

> [!NOTE]
> 执行这些步骤后，可能会登录，但帐户将处于筛选状态。 处于筛选状态时，只有帐户的默认租户和资源可用。 所有其他Azure Active Directory租户和资源将无法访问，但你可以[手动将其添加回](#how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio)。 

## <a name="how-to-opt-out-of-using-a-specific-azure-active-directory-tenant-in-visual-studio"></a>如何在 Visual Studio 中选择退出使用特定的 Azure Active Directory 租户

Visual Studio 2019 版本 16.6 及更高版本可以灵活地单独筛选租户或全局租户，从而有效地将其隐藏在Visual Studio中。 筛选出特定租户后，无需再向该租户进行身份验证，但这也意味着你将无法访问任何关联资源。

当你有多个租户并且想要通过面向特定的子集来优化开发环境时，此功能很有用。 在无法验证特定 CA/MFA 策略的情况下，此功能也很有用，因为你可以筛选出违规的租户。 

### <a name="how-to-filter-out-all-tenants"></a>如何筛选掉所有租户
若要全局筛选出所有租户，请打开“帐户设置”对话框，**(“文件>帐户设置...”>帐户选项)** 并取消选中 **“跨所有 Azure Active Directory 进行身份验证**”复选框。

取消选中该选项可以确保只对帐户的默认租户进行身份验证。 这也意味着你无法访问任何与你的帐户在其中充当来宾的其他租户关联的任何资源。

### <a name="how-to-filter-out-individual-tenants"></a>如何筛选掉单个租户
若要筛选与Visual Studio帐户关联的租户，请打开“帐户设置”对话框，**(文件>帐户设置...)** 并单击“**应用”筛选器**。 
</br>
</br>

:::image type="content" source="media/vs-2022/apply-filter.png" alt-text="应用筛选器。" border="false":::

此时将显示“筛选帐户”对话框，让你选择要与帐户一起使用的租户。 

:::image type="content" source="media/vs-2022/select-filter-account.png" alt-text="选择要筛选的帐户。":::

取消选择要筛选的租户后，**“帐户设置**”和 **“筛选器帐户**”对话框将显示筛选状态。

:::image type="content" source="media/vs-2022/account-settings-filter-account-dialogs-tenants-filtered-out-state.png" alt-text="显示“帐户设置”和“筛选帐户”对话框上筛选的租户状态的屏幕截图":::

## <a name="see-also"></a>另请参阅

- [登录 Visual Studio](signing-in-to-visual-studio.md)
- [登录 Visual Studio for Mac](/visualstudio/mac/signing-in)