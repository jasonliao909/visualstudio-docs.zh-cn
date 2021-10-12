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
ms.openlocfilehash: 0cee8215f049b0a6a50e94797ac3556deeaaacaf
ms.sourcegitcommit: d63ba1eff845d41ca095efb14b499ea96c4b6eba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129561017"
---
# <a name="update-visual-studio-to-the-most-recent-release"></a>请将 Visual Studio 更新到最新版本

::: moniker range="vs-2017"

建议更新到[最新版本](/visualstudio/releasenotes/vs2017-relnotes/)的 Visual Studio 2017，以便始终获得最新功能、修复和改进。

若要体验最新版本，建议下载并安装 [Visual Studio 2019](https://visualstudio.microsoft.com/downloads)。

> [!IMPORTANT]
> 若要安装、更新或修改 Visual Studio，必须使用具有管理权限的帐户登录。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。
>
> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[更新 Visual Studio for Mac](/visualstudio/mac/update)。

## <a name="update-visual-studio-2017-version-156-or-later"></a>更新 Visual Studio 2017 版本 15.6 或更高版本

已经简化了安装和更新体验，以便更轻松地在 IDE 中直接使用。 下面介绍了如何从版本 15.6 以及更高版本更新到较新版本的 Visual Studio。

### <a name="using-the-notifications-hub"></a>使用“通知”中心

当有更新时，Visual Studio 中会有相应的“通知”标志。

1. 保存所有内容。

1. 选择“通知”标志打开“通知”  中心，然后选择要安装的更新。

   ![显示 Visual Studio IDE“通知”中心中的更新的屏幕截图。](media/vs-install-notifications-hub-15dot6.png "Visual Studio 2017 中的通知中心")

      > [!TIP]
      > Visual Studio 2017 版本的更新是累积的，因此始终选择安装具有最新版本号的版本。

1. 当“更新”  对话框打开，请选择“立即更新”  。

    ![显示从 Visual Studio 2017“通知”中心启动的“更新”对话框中“立即更新”按钮的屏幕截图。](media/vs-update-now-from-notifications-hub.png "Visual Studio 通知中心的“更新”对话框")

     如果“用户访问控制”对话框打开，选择“是”  。 接下来，“请稍候”对话框可能会打开一段时间，然后 Visual Studio 安装程序会打开以启动更新。

     ![显示版本 15.6 中的新 Visual Studio 安装程序体验的屏幕截图。](media/visual-studio-15dot6-installer.png "版本 15.6 中的新 Visual Studio 安装程序体验")

     更新将继续。 然后，完成时，将重新启动 Visual Studio。

     > [!NOTE]
     > 当以管理员模式运行 Visual Studio 时，必须在更新后手动重启 Visual Studio。

### <a name="using-the-ide"></a>使用 IDE

可以查看更新，然后从 Visual Studio 菜单栏安装更新。

1. 保存所有内容。

1. 选择“帮助”  >“检查更新”  。

     ![显示 Visual Studio 版本 15.6 中的新“帮助”菜单的屏幕截图。](media/vs-help-menu-check-for-updates.png "Visual Studio 版本 15.6 中的新“帮助”菜单")

1. 当“更新”  对话框打开，请选择“立即更新”  。

   更新将启动（如上一节中所述），然后 Visual Studio 会在更新成功完成后重启。

   > [!NOTE]
   > 当以管理员模式运行 Visual Studio 时，必须在更新后手动重启 Visual Studio。

### <a name="using-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

和 Visual Studio 的早期版本一样，可以使用 Visual Studio 安装程序来安装更新。

1. 保存所有内容。

1. 打开安装程序。 Visual Studio 安装程序可能需要更新才能继续。

   > [!NOTE]
   > 在运行 Windows 10 或更高版本的计算机上，可以在字母“V”下找到“Visual Studio 安装程序”，也可以在字母“M”下找到“Microsoft Visual Studio 安装程序”。

1. 在安装程序中的“产品”  页上，查找先前已安装的 Visual Studio 版本。

1. 若有更新，会看到“更新”  按钮。 （可能需要等待几秒钟的时间，安装程序才能确定是否有更新。）

   选择“更新”  按钮来安装更新。

     ![显示 Visual Studio 安装程序中可用于更新 Visual Studio 2017 的“更新”按钮的屏幕截图。](media/update-visual-studio.png "使用 Visual Studio 安装程序更新 Visual Studio 2017")

## <a name="update-visual-studio-2017-version-155-or-earlier"></a>更新 Visual Studio 2017 版本 15.5 或更早版本

如果使用的是早期版本，下面将介绍如何应用从 Visual Studio 2017 版本 15.0 到版本 15.5 的更新。

### <a name="update-by-using-the-notifications-hub"></a>使用“通知”中心进行更新

1. 当有更新时，Visual Studio 中会有相应的“通知”标志。

   ![显示 Visual Studio 2017 中指示更新可用的“通知”标志的屏幕截图。](media/notification-flag.png "Visual Studio 中的更新通知标志")

   选择通知标志，打开“通知”  中心。

   ![显示带有一条通知的 Visual Studio 2017“通知”中心的屏幕截图。](media/notifications-hub.png "通知中心中的 Visual Studio 2017 更新")

      > [!TIP]
      > Visual Studio 2017 版本的更新是累积的，因此始终选择安装具有最新版本号的版本。

1. 选择“有‘Visual Studio 更新’”  ，随即会打开“扩展和更新”  对话框。

   ![显示 Visual Studio 2017“通知”中心有一条更新通知的屏幕截图。](media/notifications-hub-select.png "选择 Visual Studio 更新")

1. 在“扩展和更新”  对话框中，选择“更新”  按钮。

   ![显示“扩展和更新”对话框窗口中的更新的屏幕截图。](media/notifications-extensions-and-updates.png "Visual Studio 中的“扩展和更新”对话框")

#### <a name="more-about-visual-studio-notifications"></a>Visual Studio 通知的详细信息

Visual Studio 自身或安装的任何组件有更新时，以及 Visual Studio 环境中发生某些事件时，Visual Studio 都会通知你。

* 通知标志呈黄色时，表示有 Visual Studio 产品更新可供安装。
* 通知标志呈红色时，表示许可证有问题。
* 通知标志呈黑色时，表示有要查看的可选消息或信息性消息。

选择通知标志，打开“通知”  中心，然后选择想要对其执行操作的通知。 或选择忽略或消除通知。

 ![显示“通知”中心中的可选消息或信息性消息的屏幕截图。](media/notification-flag-optional.png "Visual Studio 中的可选或信息性消息通知标志")

如果选择忽略通知，Visual Studio 将不再显示它。 如果要重置忽略通知的列表，请选择“通知”中心中的“设置”  按钮。

   ![显示“通知”中心（用于查看“通知”选项）中的“设置”按钮的屏幕截图。](media/vs-notifications-hub-settings-button.png "选择通知中心的“设置”按钮查看“通知”选项")

### <a name="update-by-using-the-visual-studio-installer"></a>使用 Visual Studio 安装程序进行更新

1. 打开安装程序。 可能需要先更新安装程序，然后才能继续操作。 如果是这种情况，系统会提示你更新安装程序。

   > [!NOTE]
   > 在运行 Windows 10 或更高版本的计算机上，可以在字母“V”下找到“Visual Studio 安装程序”，也可以在字母“M”下找到“Microsoft Visual Studio 安装程序”。

1. 在安装程序中的“产品”  页上，查找先前已安装的 Visual Studio 版本。

1. 若有更新，会看到“更新”  按钮。 （可能需要等待几秒钟的时间，安装程序才能确定是否有更新。）

   选择“更新”  按钮来安装更新。

     ![显示 Visual Studio 安装程序中可用于更新 Visual Studio 2017 的“更新”按钮的屏幕截图。](media/update-visual-studio.png "使用 Visual Studio 安装程序更新 Visual Studio")

::: moniker-end

::: moniker range="vs-2019"

建议更新到[最新版本](/visualstudio/releases/2019/release-notes/)的 Visual Studio，以便始终获得最新功能、修复和改进。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。 如果当前使用其他版本的 Visual Studio，可以[并行安装 Visual Studio 版本](../install/install-visual-studio-versions-side-by-side.md)或[卸载以前版本的 Visual Studio](../install/uninstall-visual-studio.md)。

> [!IMPORTANT]
> 若要安装、更新或修改 Visual Studio，必须使用具有管理权限的帐户登录。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。
>
> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[更新 Visual Studio for Mac](/visualstudio/mac/update)。

下面是 Visual&nbsp;Studio&nbsp;2019 的更新方法。

## <a name="use-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

1. 在计算机上找到 Visual Studio 安装程序。

   在 Windows“开始”菜单中，可以搜索“安装程序”。

   ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2019/visual-studio-installer.png "搜索 Visual Studio 安装程序")

   可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本。

   例如，如果以前安装了 Visual&nbsp;Studio Community&nbsp;2019，并且具有该版本的更新，则安装程序中将显示“更新可用”消息。

     ![显示有可用更新的 Visual Studio 2019 安装的屏幕截图。](media/vs-2019/vs-installer-update-visual-studio-community.png "选择要更新的 Visual Studio 2019 版本")

1. 选择“更新”，以安装更新。

    ![显示 Visual Studio 安装程序中可用于更新到 Visual Studio 2019 安装的“更新”按钮的屏幕截图。](media/vs-2019/vs-installer-choose-update-visual-studio-community.png "选择“更新”按钮来安装更新")

1. 更新完成后，系统可能会要求你重新启动计算机。 如果是这样，请执行该操作，然后像往常一样启动 Visual Studio。

   如果系统不要求你重新启动计算机，请选择“启动”以从安装程序启动 Visual Studio。

    ![显示 Visual Studio 安装程序中可用于启动 Visual Studio 2019 的“启动”按钮的屏幕截图。](media/vs-2019/choose-launch-visual-studio-community.png "选择“启动”按钮启动 Visual Studio")

## <a name="use-the-ide"></a>使用 IDE

可以查看更新，然后使用 Visual Studio 2019 中的菜单栏或搜索框安装更新。

### <a name="open-visual-studio"></a>打开 Visual Studio

1. 在 Windows“开始”菜单上，选择“Visual Studio 2019”。

    ![显示在 Visual Studio IDE“开始”窗口搜索 Visual Studio 2019 后出现的结果的屏幕截图。](media/vs-2019/vs-installer-visual-studio-2019.png "从 Windows 打开 Visual Studio 2019")

1. 在“开始使用”下，选择任意选项以打开 IDE。

    ![显示 Visual Studio 安装程序的屏幕截图。](media/vs2019-choose-option-from-get-started.png "打开 Visual Studio 安装程序")

    Visual Studio 随即打开。 在 IDE 中，将简要显示“Visual Studio 2019 更新”消息。

    ![显示 IDE 中的“Visual Studio 2019 更新”消息的屏幕截图。](media/vs-2019/update-visual-studio-ide-message.png "IDE 中的“Visual Studio 2019 更新”消息")

1. 在“Visual Studio 2019 更新”消息中，选择“查看详细信息”。

   ![“Visual Studio 2019 IDE 更新”消息中的“查看详细信息”按钮的屏幕截图。](media/vs-2019/update-visual-studio-ide-view-details.png "在“Visual Studio 2019 更新”消息中，选择“查看详细信息”按钮")

1. 在“已下载更新并准备安装”对话框中，选择“更新”。

     ![显示“已下载更新并准备安装”对话框中的“更新”按钮的屏幕截图。](media/vs-2019/update-ready-install-visual-studio-community-from-ide.png "在“已下载更新并准备安装”对话框中，选择“更新”按钮")

   Visual Studio 将更新、关闭然后重新打开。

### <a name="in-visual-studio"></a>在 Visual Studio 中

1. 在菜单栏上，选择“帮助”，然后选择“检查更新”。

     ![显示“帮助”菜单中的“检查更新”的屏幕截图。](media/vs-2019/vs-ide-check-updates-help-menu.png "从“帮助”菜单中选择“检查更新”")

    > [!NOTE]
    > 还可以使用 IDE 中的搜索框来检查更新。 按 Ctrl+Q，键入“检查更新”，然后选择匹配的搜索结果。

1. 在“更新可用”对话框中，选择“更新”。

     ![显示“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2019/update-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

   Visual Studio 将更新、关闭然后重新打开。

## <a name="use-the-notifications-hub"></a>使用“通知”中心

1. 在 Visual Studio 中，保存所做的工作。

1. 从 Visual Studio IDE 的右下角选择通知图标，以打开“通知”中心。

   ![显示 Visual Studio IDE 中的“通知”图标的屏幕截图。](media/vs-2019/notification-bar.png "Visual Studio IDE 中的通知图标")

1. 在“通知中心”中，选择要安装的更新，然后选择“查看详细信息”。

     ![显示 Visual Studio 2019 中的“通知”中心的屏幕截图。](media/vs-2019/notification-hub-update.png "Visual Studio 2019 中的通知中心")

      > [!TIP]
      > Visual Studio 2019 版本的更新是累积的，因此始终选择安装具有最新版本号的版本。

1. 在“更新可用”对话框中，选择“更新”。

   Visual Studio 将更新、关闭然后重新打开。

## <a name="customize-update-settings"></a>自定义更新设置

可以通过几种不同的方式在 Visual Studio 中自定义更新设置，比如更改安装模式和选择自动下载。

有两种安装模式可供选择：

* **在下载时安装**
* **全部下载后再安装**

还可以选择“自动下载更新”设置，该设置允许在计算机处于空闲状态时下载更新。

以下是操作方法：

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 展开“环境”，然后选择“生产更新”。

    ![显示 Visual Studio 中的更新设置的屏幕截图。](media/vs-2019/update-settings-options.png)

1. 选择安装模式和 Visual Studio 更新所需的自动下载选项。

::: moniker-end

::: moniker range=">=vs-2022"

建议更新到[最新版本](/visualstudio/releases/2022/release-notes-preview)的 Visual Studio，以便始终获得最新功能、修复和改进。

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。 如果你当前使用其他版本的 Visual Studio，可以[并行安装 Visual Studio 版本](../install/install-visual-studio-versions-side-by-side.md)或[卸载以前版本的 Visual Studio](../install/uninstall-visual-studio.md)。

> [!IMPORTANT]
> 若要安装、修改或更新 Visual Studio，必须以管理员身份运行 Visual Studio 安装程序。 如果你尝试以普通用户身份修改 Visual Studio，你将收到用户帐户控制通知，提示你输入管理员凭据。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。
>
> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[更新 Visual Studio for Mac](/visualstudio/mac/update)。

下面提供更新 Visual Studio 2022 的方法。

## <a name="use-the-visual-studio-installer"></a>使用 Visual Studio 安装程序

1. 在计算机上找到 Visual Studio 安装程序。

   在 Windows 的“开始”菜单中，搜索“安装程序”，然后从结果中选择“Visual Studio 安装程序”。

   ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2022/vs-installer.png "搜索 Visual Studio 安装程序")

   > [!NOTE]
   > 还可以在以下位置中找到 Visual Studio 安装程序：
   >
   > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

   如果系统提示先更新 Visual Studio 安装程序后再继续，请按照提示进行操作。

1. 在 Visual Studio 安装程序中，查找要更新的 Visual Studio 的安装。 

   例如，如果以前安装了 Visual Studio Community 2022 Preview，并且具有该版本的更新，则 Visual Studio 安装程序中将显示“有可用更新”消息。

     ![显示有新的更新可用时 Visual Studio 安装程序中的“更新”按钮和消息的屏幕截图。](media/vs-2022/vs-installer-update-visual-studio-community.png "选择要更新的 Visual Studio 2022 版本")

1. 选择“更新”以安装更新。

    ![显示可选择安装新更新的“更新”按钮的屏幕截图。](media/vs-2022/vs-installer-choose-update-visual-studio-community.png "选择“更新”按钮以安装更新")

1. 更新完成后，Visual Studio 安装程序可能会提示你重启计算机。 如果是这样，请执行该操作，然后像往常一样启动 Visual Studio。

    如果系统不要求你重启计算机，请选择“启动”以从 Visual Studio 安装程序启动 Visual Studio。

    ![显示可选择启动 Visual Studio 的“启动”按钮的屏幕截图。](media/vs-2022/vs-installer-choose-launch-visual-studio-community.png "选择“启动”按钮启动 Visual Studio")

## <a name="use-the-visual-studio-ide"></a>使用 Visual Studio IDE

可以查看更新，然后使用 Visual Studio 2022 中的菜单栏或搜索框安装更新。

### <a name="open-visual-studio"></a>打开 Visual Studio

1. 在 Windows 的“开始”菜单上，选择“Visual Studio 2022 Preview” 。

    ![显示 Windows 10 的“开始”菜单中 Visual Studio 2022 Preview 条目的屏幕截图。](media/vs-2022/ide-start-menu.png "从 Windows 打开 Visual Studio 2022 Preview")

1. 在“开始”窗口中的“开始”下，选择任意选项以打开 Visual Studio IDE。

    ![显示 Visual Studio IDE 中的“开始”窗口的屏幕截图。](media/vs-2022/choose-option-from-get-started.png "打开 Visual Studio IDE")

    Visual Studio 随即打开。 在 Visual Studio IDE 中，将简要显示“Visual Studio 2022 更新”消息。

    ![在 Visual Studio IDE 的右下角显示 Visual Studio 2022 的更新消息的屏幕截图。](media/vs-2022/update-visual-studio-ide-message.png "IDE 中的“Visual Studio 2022 更新”消息")

1. 在“Visual Studio 2022 更新”消息中，选择“查看详细信息”。

   ![显示 Visual Studio IDE 中 Visual Studio 2022 更新通知的“查看详细信息”按钮的屏幕截图。](media/vs-2022/update-visual-studio-ide-view-details.png "在“Visual Studio 2022 更新”消息中，选择“查看详细信息”按钮")

1. 在“更新可用”对话框中，选择“更新”。

     ![显示 Visual Studio 2022 中“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2022/update-ready-install-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

   Visual Studio 将更新、关闭然后重新打开。

### <a name="in-visual-studio"></a>在 Visual Studio 中

1. 在菜单栏上，选择“帮助”，然后选择“检查更新”。

     ![显示“帮助”菜单中“检查更新”选项的屏幕截图。](media/vs-2022/ide-check-updates-help-menu.png "从“帮助”菜单中选择“检查更新”")

    > [!NOTE]
    > 还可使用 Visual Studio IDE 中的搜索框来检查更新。 按 Ctrl+Q，键入“检查更新”，然后选择匹配的搜索结果。

1. 在“更新可用”对话框中，选择“更新”。

     ![显示“有可用更新”对话框中的“更新”按钮的屏幕截图。](media/vs-2022/update-visual-studio-community-from-ide.png "在“可用更新”对话框中选择“更新”按钮")

   Visual Studio 将更新、关闭然后重新打开。

## <a name="use-the-notifications-hub"></a>使用“通知”中心

1. 在 Visual Studio 中，保存所做的工作。

1. 从 Visual Studio IDE 的右下角选择“通知”图标，打开“通知”中心。

   ![显示 Visual Studio IDE 中的“通知”图标的屏幕截图。](media/vs-2022/notification-bar.png "Visual Studio 2022 中的“通知”图标")

1. 在“通知中心”中，选择要安装的更新，然后选择“查看详细信息”。

     ![显示 Visual Studio IDE 中的“通知”中心的屏幕截图。](media/vs-2022/notification-hub-update.png "Visual Studio 2022 中的“通知”中心")

      > [!TIP]
      > Visual Studio 2022 各版本的更新是累积的，因此请始终选择安装具有最新版本号的更新。

1. 在“更新可用”对话框中，选择“更新”。

   Visual Studio 将更新、关闭然后重新打开。

## <a name="customize-update-settings"></a>自定义更新设置

可通过几种不同的方式在 Visual Studio 中自定义更新设置，比如更改安装模式或选择自动下载。

有两种安装模式可供选择：

* **在下载时安装**
* **全部下载后再安装**

还可选择“自动下载更新”选项，让 Visual Studio 在计算机处于空闲状态时自动下载更新。

以下是操作方法：

1. 在菜单栏上，依次选择“工具”>“选项”。

1. 展开“环境”，然后选择“生产更新”。

    ![显示 Visual Studio IDE 的“选项”窗口中的“更新设置”的屏幕截图。](media/vs-2022/update-settings-options.png)

1. 选择安装模式和 Visual Studio 更新所需的自动下载选项。

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
