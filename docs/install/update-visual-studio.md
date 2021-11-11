---
title: 更新 Visual Studio
titleSuffix: ''
description: 了解如何逐步将 Visual Studio 更新到最新版本。
ms.date: 09/14/2021
ms.custom: vs-acquisition
ms.topic: how-to
ms.prod: visual-studio-windows
ms.technology: vs-installation
helpviewer_keywords:
- update [Visual Studio]
- change [Visual Studio]
f1_keywords:
- VS.ToolsOptionsPages.Environment.ProductUpdates
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4747792137eca0745d2d005c441c6a3c045df0be
ms.sourcegitcommit: 67dc39e93c86ba50eb5ca877b0471fb8ab8475ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2021
ms.locfileid: "132001615"
---
# <a name="update-visual-studio"></a>更新 Visual Studio

本主题讨论了如何更新 Visual Studio 的客户端安装。  如果你是 IT 管理员，并且想要将组织的客户端配置为从网络布局进行更新，请参阅 [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)，尤其是有关[管理和更新网络安装](../install/update-a-network-installation-of-visual-studio.md)的部分。

本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[更新 Visual Studio for Mac](/visualstudio/mac/update)。 

## <a name="before-you-update"></a>更新之前

为了安装、更新或修改 Visual Studio，必须使用具有管理权限的帐户登录计算机。 如果以典型用户身份登录并尝试执行其中一个命令，则你会收到用户帐户控制通知，提示你输入管理员凭据。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。

强烈建议在执行更新之前保存工作。

计算机上必须安装了 Visual Studio 才能进行更新。 若要从 Microsoft 托管的服务器安装最新版本的 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页。 如果当前正在使用 Visual Studio 的另一个实例，可以[将 Visual Studio 的新实例并行安装到现有安装中](../install/install-visual-studio-versions-side-by-side.md)，也可以在安装此新实例之前[卸载 Visual Studio 的上一个实例](../install/uninstall-visual-studio.md)。

::: moniker range="vs-2017"

建议更新到[最新版本](/visualstudio/releasenotes/vs2017-relnotes/)的 Visual Studio 2017，以便始终获得最新功能、安全修复和改进。 若要体验最新版本，建议下载并安装 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)。

## <a name="use-the-notifications-hub"></a>使用“通知”中心

1. 当有更新时，Visual Studio IDE 的标题栏中会有相应的“通知”标志。 选择“通知”标志打开“通知”  中心，然后选择要安装的更新。

   ![显示 Visual Studio IDE“通知”中心中的更新的屏幕截图。](media/vs-install-notifications-hub-15dot6.png "Visual Studio 2017 中的通知中心")

1. 当“更新”  对话框打开，请选择“立即更新”  。

    ![显示从 Visual Studio 2017“通知”中心启动的“更新”对话框中“立即更新”按钮的屏幕截图。](media/vs-update-now-from-notifications-hub.png "Visual Studio 通知中心的“更新”对话框")

     如果“用户访问控制”对话框打开，选择“是”  。 接下来，“请稍候”对话框可能会打开一段时间，然后 Visual Studio 安装程序会打开以启动更新。

     ![显示 Visual Studio 安装程序体验的屏幕截图。](media/visual-studio-15dot6-installer.png "新 Visual Studio 安装程序体验")

     更新将完成，然后 Visual Studio 重新启动。

## <a name="manually-check-for-updates"></a>手动检查更新

1. 可以通过选择菜单栏上的“帮助”>“检查更新”来检查更新是否可用 。

     ![屏幕截图显示 Visual Studio 中的“帮助”菜单。](media/vs-help-menu-check-for-updates.png "Visual Studio 中的新“帮助”菜单")

1. 当“更新”  对话框打开，请选择“立即更新”  。

   更新将启动（如上一节中所述），然后 Visual Studio 会在更新成功完成后重启。

## <a name="use-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

1. 和 Visual Studio 的早期版本一样，可以使用 Visual Studio 安装程序来安装更新。  首先，在计算机上找到 Visual Studio 安装程序。  在 Windows“开始”菜单中，可以搜索“安装程序”。  

1. 打开安装程序。 Visual Studio 安装程序可能需要更新才能继续。

1. 在安装程序中的“产品”页上，查找先前已安装并且现在想要更新的 Visual Studio 版本。

1. 若有更新，会看到“更新”  按钮。 （可能需要等待几秒钟的时间，安装程序才能确定是否有更新。）

   选择“更新”  按钮来安装更新。

     ![显示 Visual Studio 安装程序中可用于更新 Visual Studio 2017 的“更新”按钮的屏幕截图。](media/update-visual-studio.png "使用 Visual Studio 安装程序更新 Visual Studio 2017")

::: moniker-end

::: moniker range="vs-2019"

建议更新到[最新版本](/visualstudio/releases/2019/release-notes/)的 Visual Studio 2019，以便始终获得最新功能、修复和改进。 若要体验最新版本，建议下载并安装 [Visual Studio 2022](https://visualstudio.microsoft.com/downloads)。

有几种不同的方法可以更新 Visual Studio 的安装。 可以通过 Visual Studio 安装程序更新，可以在 IDE 中检查更新或使用通知中心，或者可以通过运行[特定版本的引导程序](/visualstudio/releases/2019/history)进行更新。 下面介绍如何使用这些各种方法更新 Visual &nbsp; Studio &nbsp; 2019。

## <a name="use-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

1. 在计算机上找到 Visual Studio 安装程序。

   在 Windows“开始”菜单中，可以搜索“安装程序”。

   ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2019/visual-studio-installer.png "搜索 Visual Studio 安装程序")

   可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找要更新的 Visual Studio 的实例。

   例如，如果以前安装了 Visual&nbsp;Studio Community&nbsp;2019，并且具有该版本的更新，则安装程序中将显示“更新可用”消息。

     ![显示有可用更新的 Visual Studio 2019 安装的屏幕截图。](media/vs-2019/vs-installer-update-visual-studio-community.png "选择要更新的 Visual Studio 2019 版本")

1. 选择“更新”，以安装更新。

    ![显示 Visual Studio 安装程序中可用于更新到 Visual Studio 2019 安装的“更新”按钮的屏幕截图。](media/vs-2019/vs-installer-choose-update-visual-studio-community.png "选择“更新”按钮来安装更新")

1. 更新完成后，系统可能会要求你重新启动计算机。 如果是这样，请执行该操作，然后像往常一样启动 Visual Studio。

   如果系统不要求你重新启动计算机，请选择“启动”以从安装程序启动 Visual Studio。

    ![显示 Visual Studio 安装程序中可用于启动 Visual Studio 2019 的“启动”按钮的屏幕截图。](media/vs-2019/choose-launch-visual-studio-community.png "选择“启动”按钮启动 Visual Studio")

## <a name="use-the-message-box-in-the-ide"></a>使用 IDE 中的消息框

1.  打开 Visual Studio 时，IDE 会检查更新是否可用。  在某些情况下，系统会短暂显示 Visual Studio 2019 更新消息。 如果要立即更新，请选择“查看详细信息”。  如果要将更新延迟到关闭 Visual Studio 时，选择“关闭时更新”。

    ![显示 IDE 中的“Visual Studio 2019 更新”消息的屏幕截图。](media/vs-2019/update-visual-studio-ide-message.png "IDE 中的“Visual Studio 2019 更新”消息")

1. 如果你选择了“查看详细信息”，那么在随后的“更新已下载并准备安装”对话框中，选择“更新”以立即更新  。

     ![显示“已下载更新并准备安装”对话框中的“更新”按钮的屏幕截图。](media/vs-2019/update-ready-install-visual-studio-community-from-ide.png "在“已下载更新并准备安装”对话框中，选择“更新”按钮")

## <a name="manually-check-for-updates"></a>手动检查更新

1. 你可以从菜单栏中选择“帮助”，然后选择“检查更新”，来检查是否有更新 。  你也可以使用搜索框，按 Ctrl+Q 键，输入“检查更新”，然后选择匹配的搜索结果 。 

     ![显示“帮助”菜单中的“检查更新”的屏幕截图。](media/vs-2019/vs-ide-check-updates-help-menu.png "从“帮助”菜单中选择“检查更新”")

1. 在“更新可用”对话框中，选择“更新”。

     ![显示“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2019/update-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

## <a name="use-the-notifications-hub"></a>使用“通知”中心

1. 从 Visual Studio IDE 的右下角选择通知图标，以打开“通知”中心。

   ![显示 Visual Studio IDE 中的“通知”图标的屏幕截图。](media/vs-2019/notification-bar.png "Visual Studio IDE 中的通知图标")

1. 在通知中心，选择要安装的更新。 如果要立即更新，请选择“查看详细信息”。 如果要将更新延迟到关闭 Visual Studio 时，选择“关闭时更新”。

     ![显示 Visual Studio 2019 中的“通知”中心的屏幕截图。](media/vs-2019/notification-hub-update.png "Visual Studio 2019 中的通知中心")

1. 如果选择“查看详细信息”，然后在后续的“有可用更新”对话框中，选择“更新”  。

## <a name="run-a-specific-bootstrapper"></a>运行特定的引导程序
如果你是 Enterprise 或 Professional 客户，可以将 Visual Studio 2019 的实例更新为已发布的任何特定版本，只要其版本高于当前安装的版本。 若要通过此方法更新 Visual Studio 2019 的实例，[导航到 Visual Studio 2019 版本历史记录页](/visualstudio/releases/2019/history)，将对应于所需更新版本的引导程序下载到产品安装目录中，然后双击它以启动更新。  

## <a name="customize-update-settings"></a>自定义更新设置

可以自定义多个不同的设置来控制更新行为。 其中一些设置是 Visual Studio 2019 本机设置，用于处理产品位的下载和安装方式及时间。 其他设置（例如配置更新源的能力）需要具有较新的 Visual Studio 2022 安装程序。  

### <a name="installation-and-download-behaviors"></a>安装和下载行为

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 展开“环境”，然后选择“生产更新”。

    ![显示 Visual Studio 中的更新设置的屏幕截图。](media/vs-2019/update-settings-options.png)

1. 观察可在此对话框中设置的配置选项。 你可以选择“自动下载更新”设置，该设置允许在计算机处于空闲状态时下载更新。 还有两种安装模式可供选择：在下载时安装，以及全部下载后再安装 。   选择安装模式和 Visual Studio 更新所需的自动下载设置。

### <a name="configure-source-location-of-updates"></a>配置更新的源位置
如果位于企业环境中，可以配置客户端实例查找更新的位置。 这适用于从网络布局安装客户端，但稍后希望客户端从其他网络布局获取更新的情况。 配置更新位置的能力要求存在较新的 Visual Studio 2022 安装程序，该安装程序可通过在客户端计算机上安装 Visual Studio 2022 或由管理员通过网络布局推送来获取。 若要详细了解如何配置此方案，请参阅 [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)

## <a name="update-on-close"></a>关闭时更新

在 Visual Studio 2019 版本 16.9 中，我们引入了“关闭时更新”的概念。  当更新可用时，IDE 中的更新通知 UI 提供了一种方法，可以将更新推迟到在自愿关闭 Visual Studio 时。 “关闭时更新”按钮将显示在更新通知消息框中，还可以在通知中心进行选择。 “关闭时更新”命令不是永久设置；它仅适用于当前更新。 换句话说，在每次确认或取消有可用更新的通知时，必须选择“关闭时更新”延迟。

   ![屏幕截图显示更新通知消息框中的“关闭时更新”选项。](media/vs-2019/update-on-close.png)

::: moniker-end

::: moniker range=">=vs-2022"

建议更新到[最新版本](/visualstudio/releases/2022/release-notes)的 Visual Studio 2022，以便始终获得最新功能、修复和改进。

有几种不同的方法可以更新 Visual Studio 的安装。 可以通过 Visual Studio 安装程序更新，可以在 IDE 中检查更新或使用通知中心，或者可以通过运行[特定版本的引导程序](/visualstudio/releases/2022/release-history)进行更新。 下面介绍如何使用这些各种方法更新 Visual &nbsp; Studio &nbsp; 2022。

## <a name="use-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

1. 在计算机上找到 Visual Studio 安装程序。

   在 Windows 的“开始”菜单中，搜索“安装程序”，然后从结果中选择“Visual Studio 安装程序”。

   ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2022/vs-installer.png "搜索 Visual Studio 安装程序")

   如果系统提示先更新 Visual Studio 安装程序后再继续，请按照提示进行操作。

1. 在 Visual Studio 安装程序中，查找要更新的 Visual Studio 的安装。 

   例如，如果以前安装了 Visual Studio Community 2022 Preview，并且具有该版本的更新，则 Visual Studio 安装程序中将显示“有可用更新”消息。

     ![显示有新的更新可用时 Visual Studio 安装程序中的“更新”按钮和消息的屏幕截图。](media/vs-2022/vs-installer-update-visual-studio-community.png "选择要更新的 Visual Studio 2022 版本")

1. 选择“更新”以安装更新。

    ![显示可选择安装新更新的“更新”按钮的屏幕截图。](media/vs-2022/vs-installer-choose-update-visual-studio-community.png "选择“更新”按钮以安装更新")

1. 更新完成后，Visual Studio 安装程序可能会提示你重启计算机。 如果是这样，请执行该操作，然后像往常一样启动 Visual Studio。

    如果系统不要求你重启计算机，请选择“启动”以从 Visual Studio 安装程序启动 Visual Studio。

    ![显示可选择启动 Visual Studio 的“启动”按钮的屏幕截图。](media/vs-2022/vs-installer-choose-launch-visual-studio-community.png "选择“启动”按钮启动 Visual Studio")

## <a name="use-the-message-box-in-the-ide"></a>使用 IDE 中的消息框

1. 打开 Visual Studio 时，IDE 会检查更新是否可用。  在某些情况下，系统会短暂显示 Visual Studio 2022 更新消息。 如果要立即更新，请选择“查看详细信息”。  如果要将更新延迟到关闭 Visual Studio 时，选择“关闭时更新”。

    ![在 Visual Studio IDE 的右下角显示 Visual Studio 2022 的更新消息的屏幕截图。](media/vs-2022/update-visual-studio-ide-message.png "IDE 中的“Visual Studio 2022 更新”消息")

1. 如果选择“查看详细信息”，然后在后续的“有可用更新”对话框中，选择“更新”以立即更新  。 

     ![显示 Visual Studio 2022 中“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2022/update-ready-install-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

## <a name="manually-check-for-updates"></a>手动检查更新

1. 你可以从菜单栏中选择“帮助”，然后选择“检查更新”，来检查是否有更新 。  你也可以使用搜索框，按 Ctrl+Q 键，输入“检查更新”，然后选择匹配的搜索结果 。 

     ![显示“帮助”菜单中“检查更新”选项的屏幕截图。](media/vs-2022/ide-check-updates-help-menu.png "从“帮助”菜单中选择“检查更新”")

1. 在“更新可用”对话框中，选择“更新”。

     ![显示“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2022/update-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

## <a name="use-the-notifications-hub"></a>使用“通知”中心

1. 从 Visual Studio IDE 的右下角选择“通知”图标，打开“通知”中心。

   ![显示 Visual Studio IDE 中的“通知”图标的屏幕截图。](media/vs-2022/notification-bar.png "Visual Studio 2022 中的“通知”图标")

1. 在通知中心，选择要安装的更新。 如果要立即更新，请选择“查看详细信息”。 如果要将更新延迟到关闭 Visual Studio 时，选择“关闭时更新”。

     ![显示 Visual Studio IDE 中的“通知”中心的屏幕截图。](media/vs-2022/notification-hub-update.png "Visual Studio 2022 中的“通知”中心")

1. 如果选择“查看详细信息”，然后在后续的“有可用更新”对话框中，选择“更新”  。

## <a name="run-a-specific-bootstrapper"></a>运行特定的引导程序
如果你是 Enterprise 或 Professional 客户，可以将 Visual Studio 2022 的实例更新为已发布的任何特定版本，只要其版本高于当前安装的版本。 若要通过此方法更新 Visual Studio 2022 的实例，[导航到 Visual Studio 2022 版本历史记录页](/visualstudio/releases/2022/release-history)，将对应于所需更新版本的引导程序下载到产品安装目录中，然后双击它以启动更新。

## <a name="customize-update-settings"></a>自定义更新设置

可以自定义多个不同的设置来控制更新行为，例如如何以及何时下载和安装产品位，或者更新源的位置。  

### <a name="installation-and-download-behaviors"></a>安装和下载行为

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 展开“环境”，然后选择“生产更新”。

    ![显示 Visual Studio IDE 的“选项”窗口中的“更新设置”的屏幕截图。](media/vs-2022/update-settings-options.png)

1. 观察可在此对话框中设置的配置选项。 你可以选择“自动下载更新”设置，该设置允许在计算机处于空闲状态时下载更新。 还有两种安装模式可供选择：在下载时安装，以及全部下载后再安装 。   选择安装模式和 Visual Studio 更新所需的自动下载设置。

### <a name="configure-source-location-of-updates"></a>配置更新的源位置
使用 Visual Studio 2022，现在可以配置客户端从何处获取更新。 这些更新源位置被称为“通道“，你可以在[Visual Studio 发行节奏](/visualstudio/productinfo/release-rhythm)文档中找到更多关于通道目的和可用性的信息。 Microsoft 向所有人提供最新版和预览版通道，并且长期服务通道 (LTSC) 可供 Enterprise 和 Professional 客户使用。 IT 管理员还可以配置客户端应有权访问的更新源位置，例如网络布局。 请参考 [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)，了解其他选项和如何设置的细节。 

有两种方法可以打开“更新设置”对话框，这允许你更改 Visual Studio 实例应获取更新的通道。 

1. 打开 Visual Studio 安装程序，选择要配置的实例，选择“更多”按钮，然后选择“更新设置”菜单选项 。 请参阅前面的说明，了解如何查找 Visual Studio 安装程序。

    ![屏幕截图显示安装程序中的更新设置。](media/vs-2022/installer-update-settings-menu-option.png)

2. 调用“更新设置”对话框的另一种方法是打开 Visual Studio IDE，打开“有可用更新”对话框（更新通知上的“查看详细信息”或“帮助”菜单上的“检查更新”），然后单击“更改更新设置”链接 。   

    ![屏幕截图显示 IDE 中“有可用更新”对话框中的更新设置。](media/vs-2022/invoke-update-settings-in-the-IDE.png)
    
“更新设置”对话框将如下所示。

   ![屏幕截图显示 Visual Studio 2022 IDE 中的“更新设置”对话框。](media/vs-2022/update-settings.png)

通过在“更新通道”下拉菜单中选择正确的值，你可以控制这个 Visual Studio 实例未来更新的源位置。 其他需要记住的方面包括：
 * 预览版和最新版通道适用于所有版本的 Visual Studio，LTSC 通道仅适用于 Professional Enterprise 客户。 
 * 可以选择在配置更新通道位置后立即更新 Visual Studio 实例。 或者，可以将实际产品更新延迟到稍后的时间。 配置更新通道的行为和更新产品的行为是两个独立的事件。 
 * 更新到新通道时，将在该通道安装最新版本。 如果你是企业客户，并且想要在通道上安装特定版本，请按照前面所述的“运行特定引导程序说明”进行操作。 
 * 只有当该通道提示提供的产品版本大于你所安装的版本时，你才能改变更新通道。 例如，始终可以从最新版通道转换到预览版通道，但无法从预览版通道转换到最新版通道，除非最新版通道的最新版本超过已安装的预览版。 
 * LTSC 通道都有到期日期。 LTSC 过期后，它将不能用作更新源，并且它将从此列表中消失。
 * 所有 Microsoft 通道都托管在 Microsoft 服务器上，需要访问 Internet。
 * 每个 Visual Studio 实例都能够独立配置其源进行更新。 因此，如果安装了两个 Visual Studio 2022 实例，则每个实例都可以从不同的通道进行更新。 
 * IT 管理员可以控制“更新通道”下拉菜单中的数值。 例如，他们可以将网络布局位置添加为更新源。 他们还可以禁止 Microsoft 托管位置作为更新源选项提供。 此功能还适用于 Visual Studio 2019 安装。 若要了解如何配置这些更新位置，请参阅 [Visual Studio 管理员指南](https://aka.ms/vs/admin/guide)

## <a name="update-on-close"></a>关闭时更新

当更新可用时，IDE 中的更新通知 UI 提供了一种方法，可以将更新推迟到在自愿关闭 Visual Studio 时。 “关闭时更新”按钮将显示在更新通知消息框中，还可以在通知中心进行选择 。 “关闭时更新”命令不是永久设置；它仅适用于当前更新。 换句话说，在每次确认或取消有可用更新的通知时，必须选择“关闭时更新”延迟。

   ![屏幕截图显示更新通知消息框中的“关闭时更新”选项。](media/vs-2022/update-on-close.png)

::: moniker-end

## <a name="administrator-updates"></a>管理员更新

如果你是集中管理软件安装的组织的一员，则企业管理员可能会控制 Visual Studio 在你计算机上的更新方式。 有关如何控制或配置计算机可接受的更新类型的详细信息，请参阅[使用 Configuration Manager 部署 Visual Studio 更新](../install/applying-administrator-updates.md#using-configuration-manager-to-deploy-visual-studio-updates)。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [并行安装 Visual Studio 版本](install-visual-studio-versions-side-by-side.md)
* [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
* [Visual Studio Enterprise 指南](visual-studio-enterprise-guide.md)
* [在维修基线上更新 Visual Studio](update-servicing-baseline.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [修改 Visual Studio](modify-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
