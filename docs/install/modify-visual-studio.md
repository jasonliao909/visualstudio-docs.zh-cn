---
title: 修改 Visual Studio 工作负载、组件和语言包
titleSuffix: ''
description: 了解如何逐步修改 Visual Studio。
ms.date: 10/12/2020
ms.topic: how-to
ms.custom: contperf-fy21q2
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 30b28af562e5dbaa8c05624f6cc9d531cf652419
ms.sourcegitcommit: 8d3d51042261df603487169a7a008fe8f71404ec
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2021
ms.locfileid: "109501767"
---
# <a name="modify-visual-studio-workloads-components-and-language-packs"></a>修改 Visual Studio 工作负载、组件和语言包

::: moniker range="vs-2019"

可轻松修改 Visual Studio，使其在你需要时包含想要的内容。 为此，请打开 Visual Studio 安装程序以添加或删除工作负载和组件。

::: moniker-end

::: moniker range="vs-2017"

我们不但简化了 Visual Studio 的个性化设置，让用户能够轻松匹配所需完成的任务，还简化了 Visual Studio 的自定义操作。 要执行此操作，请打开新的 Visual Studio 安装程序，即可进行所需更改。

::: moniker-end

## <a name="prerequisites"></a>先决条件

+ 若要安装、更新或修改 Visual Studio，必须使用具有管理权限的帐户登录。 有关详细信息，请参阅[用户权限与 Visual Studio](../ide/user-permissions-and-visual-studio.md)。

+ 以下过程假定你具有 Internet 连接。 有关如何修改先前创建的 Visual Studio [脱机安装](create-an-offline-installation-of-visual-studio.md)的详细信息，请参阅[更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)页和[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)页。

## <a name="launch-the-installer"></a>启动安装程序

若要对安装进行修改，你需要启动 Visual Studio 安装程序。

::: moniker range="vs-2017"

1. 在计算机上找到 Visual Studio 安装程序。

     例如，在运行 Windows 10 的计算机上，选择“开始”，然后滚动到字母“V”，它作为“Visual Studio 安装程序”在那里列出    。

     ![Visual Studio 安装程序](media/locate-the-visual-studio-installer.png "找到 Microsoft Visual Studio 安装程序")

     >[!TIP]
     >对于某些计算机，Visual Studio 安装程序可能列在字母 **“M”** 下，即 **Microsoft Visual Studio 安装程序**。<br/><br/> 或者，可以在以下位置找到 Visual Studio 安装程序：`C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. 打开安装程序，然后选择“修改”  。

     ![启动或修改 Visual Studio](media/modify-visual-studio.png "修改 Visual Studio 2017")

     > [!IMPORTANT]
     > 如果还有更新挂起，则“修改”按钮会出现在其他位置。 这样一来，如果选择执行此操作，可以在不更新的情况下修改 Visual Studio。 单击“更多”，然后选择“修改”   。
     >
     > ![更新或修改 Visual Studio](media/modify-or-update-visual-studio.png "更新或修改 Visual Studio 2017")

::: moniker-end

::: moniker range="vs-2019"

1. 在计算机上找到 Visual Studio 安装程序。

     在 Windows“开始”菜单中，可以搜索“安装程序”。

     ![Visual Studio 安装程序](media/vs-2019/visual-studio-installer.png "搜索 Visual Studio 安装程序")

     > [!NOTE]
     > 还可以在以下位置中找到 Visual Studio 安装程序：
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    可能需要先更新安装程序，然后才能继续操作。 如果是这样，请按照提示操作。

1. 在安装程序中，查找已安装的 Visual Studio 版本，然后选择“修改”  。

     ![选择 Visual Studio 版本，然后进行修改](media/vs-2019/vs-installer-modify.png "选择 Visual Studio 2019 版本，然后进行修改")

     > [!IMPORTANT]
     > 如果还有更新挂起，则“修改”按钮会出现在其他位置。 这样一来，如果需要的话，可以在不更新的情况下修改 Visual Studio。 选择“更多”  ，然后选择“修改”  。
     >
     > ![更新或修改 Visual Studio](media/vs-2019/modify-update-visual-studio.png "更新或修改 Visual Studio 2019")

::: moniker-end

## <a name="change-workloads-or-individual-components"></a>更改工作负载或单个组件

::: moniker range="vs-2017"

 [工作负载](https://visualstudio.microsoft.com/vs/support/selecting-workloads-visual-studio-2017/)包含所用编程语言或平台必需的功能。 可以使用工作负载来修改 Visual Studio，以便在需要执行某项操作时为其提供支持。

1. 在 Visual Studio 安装程序中，选择“工作负载”  选项卡，然后选择或取消选择所需的工作负载。

   或者，如果不想使用工作负载来自定义 Visual Studio 安装，请选择“单个组件”选项卡，选中所需组件，然后按照提示操作。

    ![Visual Studio 2017 安装对话框](media/modify-workloads.png "在 Visual Studio 2019 中选择工作负载")

1. 选择是要接受默认的“下载时安装”选项还是“全部下载后再安装”选项   。

    ![Visual Studio 2017 安装选项](media/vs-2019/vs-installer-choose-install-or-download.png "选择下载时安装，或者先下载然后再安装")

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

    ![Visual Studio 2019 安装对话框](media/vs-2019/vs-installer-modify-workloads.png "在 Visual Studio 2019 中选择工作负载")

1. 选择是要接受默认的“下载时安装”选项还是“全部下载后再安装”选项   。

    ![Visual Studio 2019 安装选项](media/vs-2019/vs-installer-choose-install-or-download.png "选择下载时安装，或者先下载然后再安装")

    如果想要先下载稍后再安装，则“全部下载后再安装”选项很有用。

1. 选择“修改”  。

1. 安装完新的工作负载后，从 Visual Studio 安装程序中选择“启动”  以打开 Visual Studio。

::: moniker-end


>[!TIP]
> 有关 SQL Server Data Tools (SSDT) 组件的信息，请参阅[下载并安装 SSDT for Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15&preserve-view=true)。

## <a name="modify-language-packs"></a>修改语言包

默认情况下，安装程序首次运行时会匹配操作系统语言。 不过，你可以随时更改语言。 

为此，请执行以下操作：
1. 在 Visual Studio 安装程序中，选择“语言包”选项卡。
2. 选择首选语言。
3. 按提示操作。

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>另请参阅

* [Visual Studio 工作负载和组件 ID 列表](workload-and-component-ids.md)
* [更新 Visual Studio](update-visual-studio.md)
* [更新基于网络的 Visual Studio 安装](update-a-network-installation-of-visual-studio.md)
* [卸载 Visual Studio](uninstall-visual-studio.md)
