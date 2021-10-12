---
title: 修改 Visual Studio 工作负载、组件和语言包
titleSuffix: ''
description: 了解如何逐步修改 Visual Studio。
ms.date: 09/14/2021
ms.topic: how-to
ms.custom: vs-acquisition
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 0e679e903c797d78403d2123ddecee5d8bc22fda
ms.sourcegitcommit: d63ba1eff845d41ca095efb14b499ea96c4b6eba
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129561108"
---
# <a name="modify-visual-studio-workloads-components-and-language-packs"></a>修改 Visual Studio 工作负载、组件和语言包

::: moniker range=">=vs-2019"

可轻松修改 Visual Studio，使其在你需要时包含想要的内容。 为此，请打开 Visual Studio 安装程序，然后添加或删除工作负载、组件和语言包。

::: moniker-end

::: moniker range="vs-2017"

我们不但简化了 Visual Studio 的个性化设置，让用户能够轻松匹配所需完成的任务，还简化了 Visual Studio 的自定义操作。 要执行此操作，请打开新的 Visual Studio 安装程序，即可进行所需更改。

::: moniker-end

## <a name="prerequisites"></a>先决条件

- 若要安装、修改或更新 Visual Studio，必须以管理员身份运行 Visual Studio 安装程序。 如果你尝试以普通用户身份修改 Visual Studio，你将收到用户帐户控制通知，提示你输入管理员凭据。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。

- 以下过程假定你具有 Internet 连接。 若要详细了解如何修改以前创建的 Visual Studio 的[脱机安装](create-an-offline-installation-of-visual-studio.md)，请参阅：
  - [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
  - [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)

## <a name="launch-the-installer-to-modify-your-installation"></a>启动安装程序以修改安装

若要修改 Visual Studio 安装，首先需要启动 Visual Studio 安装程序，然后选择要修改的 Visual Studio安装。

::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 或更高版本的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出  。

     ![显示 Windows 10 的“开始”菜单中 Visual Studio 安装程序条目的屏幕截图。](media/locate-the-visual-studio-installer.png "找到 Microsoft Visual Studio 安装程序")

     >[!TIP]
     >对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。<br/><br/> 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 打开安装程序，然后选择“修改”  。

     ![显示 Visual Studio 安装程序中“修改”按钮的屏幕截图。](media/modify-visual-studio.png "修改 Visual Studio 2017")

     > [!IMPORTANT]
     > 如果还有更新挂起，则“修改”按钮会出现在其他位置。 这样一来，如果选择执行此操作，可以在不更新的情况下修改 Visual Studio。 单击“更多”，然后选择“修改”   。
     >
     > ![显示 Visual Studio 安装程序中“修改”按钮的屏幕截图，该按钮在待更新时位于“更多”下拉菜单中。](media/modify-or-update-visual-studio.png "更新或修改 Visual Studio 2017")

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     在 Windows“开始”菜单中，可以搜索“安装程序”。

     ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2019/visual-studio-installer.png "搜索 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本，然后选择“修改”  。

     ![显示 Visual Studio 安装程序中 Visual Studio 安装的列表的屏幕截图。](media/vs-2019/vs-installer-modify.png "选择 Visual Studio 2019 版本，然后进行修改")

     > [!IMPORTANT]
     > 如果还有更新挂起，则“修改”按钮会出现在其他位置。 这样一来，如果需要的话，可以在不更新的情况下修改 Visual Studio。 选择“更多”  ，然后选择“修改”  。
     >
     > ![显示 Visual Studio 安装程序中“修改”按钮的屏幕截图，该按钮在待更新时位于“更多”下拉菜单中。](media/vs-2019/modify-update-visual-studio.png "更新或修改 Visual Studio 2019")

::: moniker-end

::: moniker range=">=vs-2022"

1. 有许多方法可以打开 Visual Studio 安装程序：

   - 在 Windows 的“开始”菜单中，可以搜索“安装程序”，然后从结果中选择“Visual Studio 安装程序”。

     ![显示在“开始”菜单搜索 Visual Studio 安装程序后出现的结果的屏幕截图。](media/vs-2022/vs-installer.png "搜索 Visual Studio 安装程序")

   - 运行 Visual Studio 安装程序可执行文件，该可执行文件位于以下路径：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

   - 如果你打开了 Visual Studio，请选择“工具”>“获取工具和功能...”，这会打开 Visual Studio 安装程序。

     ![显示 Visual Studio 2022“工具”菜单的屏幕截图。](media/vs-2022/vs-tools-menu.png "Visual Studio 2022 工具菜单")

   在继续之前，系统可能会提示更新 Visual Studio 安装程序。 如果是这样，请按照提示操作。

1. 在 Visual Studio 安装程序中，查找要修改的 Visual Studio 的安装，然后选择“修改”按钮。

     ![显示 Visual Studio 安装程序中 Visual Studio 安装的列表的屏幕截图。](media/vs-2022/vs-installer-modify.png "选择要修改的 Visual Studio 安装")

::: moniker-end

## <a name="change-workloads-or-individual-components"></a>更改工作负载或单个组件

::: moniker range="vs-2017"

 [工作负载](https://visualstudio.microsoft.com/vs/support/selecting-workloads-visual-studio-2017/)包含所用编程语言或平台必需的功能。 可以使用工作负载来修改 Visual Studio，以便在需要执行某项操作时为其提供支持。

1. 在 Visual Studio 安装程序中，选择“工作负载”  选项卡，然后选择或取消选择所需的工作负载。

   或者，如果不想使用工作负载来自定义 Visual Studio 安装，请选择“单个组件”选项卡，选中所需组件，然后按照提示操作。

    ![显示 Visual Studio 安装程序“工作负载”选项卡的屏幕截图。](media/modify-workloads.png "在 Visual Studio 2017 中选择工作负载")

1. 选择是要接受默认的“下载时安装”选项还是“全部下载后再安装”选项   。

    ![显示 Visual Studio 安装程序中下载和安装选项的屏幕截图。](media/vs-2019/vs-installer-choose-install-or-download.png "选择下载时安装，或者先下载然后再安装")

    如果想要先下载稍后再安装，则“全部下载后再安装”选项很有用。

1. 选择“修改”  。

1. 如果需要，选择“工作负载”选项卡，然后选中或取消选中所需的工作负载。

1. 安装完新的工作负载后，从 Visual Studio 安装程序中选择“启动”  以打开 Visual Studio。

::: moniker-end

::: moniker range="vs-2019"

 工作负载包含所用编程语言或平台必需的功能。 可以使用工作负载来修改 Visual Studio，以便在需要执行某项操作时为其提供支持。

 > [!TIP]
>若要详细了解开发所需的工具和组件捆绑包，请参阅 [Visual Studio 工作负荷](https://visualstudio.microsoft.com/vs/#workloads)。

1. 在 Visual Studio 安装程序中，选择“工作负载”  选项卡，然后选择或取消选择所需的工作负载。

    ![显示 Visual Studio 安装程序“工作负载”选项卡的屏幕截图。](media/vs-2019/vs-installer-modify-workloads.png "在 Visual Studio 2019 中选择工作负载")

1. 选择是要接受默认的“下载时安装”选项还是“全部下载后再安装”选项   。

    ![显示 Visual Studio 安装程序中下载和安装选项的屏幕截图。](media/vs-2019/vs-installer-choose-install-or-download.png "选择下载时安装，或者先下载然后再安装")

    如果想要先下载稍后再安装，则“全部下载后再安装”选项很有用。

1. 选择“修改”  。

1. 安装完新的工作负载后，从 Visual Studio 安装程序中选择“启动”  以打开 Visual Studio。

::: moniker-end

::: moniker range=">=vs-2022"

工作负载包含所用编程语言或平台必需的组件。 可以使用工作负载来修改 Visual Studio，以便在需要执行某项操作时为其提供支持。

> [!TIP]
> 若要详细了解开发所需的工具和组件捆绑包，请参阅 [Visual Studio 工作负载](https://visualstudio.microsoft.com/vs/#workloads)。

1. 在 Visual Studio 安装程序中，选择“工作负载”  选项卡，然后选择或取消选择所需的工作负载。

    ![显示 Visual Studio 安装程序“工作负载”选项卡的屏幕截图。](media/vs-2022/vs-installer-modify-workloads.png "在 Visual Studio 安装程序中选择工作负载")

1. 若要添加的组件多于工作负载安装，请选择“单个组件”选项卡，然后根据需要选择或取消选择单个组件。

    ![显示 Visual Studio 安装程序的各组件选项卡的屏幕截图。](media/vs-2022/vs-installer-individual-components.png "在 Visual Studio 安装程序中选择单个组件")

1. 选择“下载时安装”或“全部下载”，然后安装 。 默认选项“下载时安装“通过提前启动安装来节省总体时间。

    ![显示 Visual Studio 安装程序中下载和安装选项的屏幕截图。](media/vs-2022/vs-installer-choose-install-or-download.png "在 Visual Studio 安装程序中下载和安装序列选项")

1. 选择“修改”  。

1. 安装完修改后的工作负载或组件后，从 Visual Studio 安装程序中选择“启动”以打开 Visual Studio 2022 预览版。

::: moniker-end

> [!TIP]
> 有关 SQL Server Data Tools (SSDT) 组件的信息，请参阅[下载并安装 SSDT for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15&preserve-view=true)。

## <a name="modify-language-packs"></a>修改语言包

Visual Studio 安装程序为 Visual Studio 选择与操作系统语言匹配的默认语言包。 不过，你可以随时更改默认语言。

为此，请执行以下操作：

1. 在 Visual Studio 安装程序中，选择“语言包”选项卡。
1. 选择首选语言。
1. 按提示操作。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [Visual Studio 工作负载和组件 ID 列表](workload-and-component-ids.md)
* [更新 Visual Studio](update-visual-studio.md)
* [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
