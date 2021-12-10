---
title: 更新基于网络的安装
description: 了解如何更新通过网络布局安装的 Visual Studio 客户端
ms.date: 12/7/2021
ms.topic: conceptual
helpviewer_keywords:
- '{{PLACEHOLDER}}'
- '{{PLACEHOLDER}}'
ms.assetid: 1AF69C0E-0AC9-451B-845D-AE4EDBCEA65C
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: d1961c85d6c918e9b3dcdbef9bf5511b77998186
ms.sourcegitcommit: 99e0146dfe742f6d1955b9415a89c3d1b8afe4e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2021
ms.locfileid: "134553981"
---
# <a name="update-a-visual-studio-client-that-was-installed-from-a-network-layout"></a>更新通过网络布局安装的 Visual Studio 客户端

可以并且应该定期更新所有 Visual Studio 的客户端，以便它们接收最新的安全和功能修补程序。 

如果 Visual Studio 客户端最初通过网络布局安装，则很有可能客户端计算机属于“托管环境”的一部分，这意味着它由中心管理团队控制并且必须遵守组织策略。 若要更新托管环境中的客户端计算机，请考虑以下问题，问题答案将告知你应该如何处理更新过程。 

-  更新来自何处：网络布局或 Microsoft 托管服务器？ 如果更新来自网络布局，是否已准备网络布局？
-  此更新是由用户启动，还是管理员启动的事件？ 请记住，执行更新的人员都必须具有管理员权限。

## <a name="prepare-the-update-source"></a>准备更新源

如果要通过 Microsoft 托管的服务器更新客户端，那么该客户端将在该[通道](/visualstudio/releases/2022/vs2022-release-rhythm)上下载并安装 Microsoft 提供的最新版本。 

如果要通过网络布局中更新客户端，第一步是使用更新的产品准备网络布局。 你可以[利用最新产品更新来更新现有布局](/visualstudio/install/create-a-network-installation-of-visual-studio#update-or-modify-your-layout)，以便新的安装和更新都将收到更新的版本。 或者，你可以在另外的目录中[创建全新布局](/visualstudio/install/create-a-network-installation-of-visual-studio)，以便用于更新客户端计算机。

## <a name="enable-manual-user-initiated-client-side-updates"></a>启用手动用户启动的客户端更新 
客户端计算机上拥有足够权限的用户可以[自行手动启动 Visual Studio 更新](/visualstudio/install/update-visual-studio)。 必须正确配置 Visual Studio 客户端才能在正确的源位置中找到更新，这样才可以识别更新可用。 如果更新发生时正在使用任何文件，如 Visual Studio 已打开，则需要关闭 Visual Studio 才能完成更新。 偶尔，更新将需要重启。

### <a name="manually-configure-where-the-visual-studio-client-looks-for-updates"></a>手动配置 Visual Studio 客户端查找更新的位置

Visual Studio 一开始安装在客户端计算机上时，它会记录应在何处检查更新。 如果 Visual Studio 通过 Microsoft 托管服务器安装，则默认情况下，它将从 Microsoft 托管的服务器中查找更新。 如果通过对网络布局调用引导程序来安装或更新 Visual Studio，它便将在[布局指定的位置](/visualstudio/install/automated-installation-with-response-file)中查找更新。  

::: moniker range="vs-2017"

在 Visual Studio 2017 中，客户端安装产品后，客户端的更新位置配置就会锁定，并无法更改。 若要为更新配置其他源位置，需要使用正确的布局配置卸载并重新安装该产品。

::: moniker-end

::: moniker range="vs-2019"

对于默认 Visual Studio 2019 功能，客户端安装产品后，客户端的更新位置配置就会锁定，并无法更改。 若要可靠地更改更新的源位置，唯一的方法是使用正确的配置卸载并重新安装该产品。
 
但是，如果 Visual Studio 客户端使用最新的 Visual Studio 2022 安装程序，则可以更改客户端的更新源位置。 如果希望通过一种布局安装而让更新来自另一种布局，这就很有用。 可通过两种方法将 Visual Studio 2022 安装程序安装到客户端计算机上。 最简单的方法便是安装并使用 Visual Studio 2022 产品。 或者，你可以[通过 Visual Studio 2019 布局分发 Visual Studio 2022 安装程序](/visualstudio/install/create-a-network-installation-of-visual-studio#configure-the-layout-to-always-use-the-latest-installer)。

::: moniker-end

::: moniker range=">=vs-2019"

若要手动查看和配置用于让客户端查找更新的更新位置，请打开[更新设置](/visualstudio/install/update-visual-studio?view=vs-2022&preserve-view=true#configure-source-location-of-updates-1)，确保其配置正确。 然后，你可以从客户端启动更新。  

::: moniker-end

### <a name="update-notifications"></a>更新通知

如果客户端查找更新的位置有可用的更新，客户端便会[弹出一条消息或通知标志](/visualstudio/install/update-visual-studio?#use-the-message-box-in-the-ide-1)。  

若要详细了解如何控制何时向用户显示更新通知，请参阅[控制对基于网络的 Visual Studio 部署的更新](/visualstudio/install/set-defaults-for-enterprise-deployments#controlling-notifications-in-the-visual-studio-ide)。

### <a name="manually-initiate-the-update"></a>手动启动更新

用户可以通过以下方式[手动更新](/visualstudio/install/update-visual-studio) Visual Studio 实例： 
  * 启动 Visual Studio 安装程序。 如果更新可用，则可以单击“更新”。
  * 启动 Visual Studio IDE 并响应通知标志或消息，或者选择“帮助”/“检查”获取更新。  

## <a name="programatically-update-the-client-machines"></a>以编程方式更新客户端计算机
管理员可以通过向客户端安装程序发出Visual Studio或调用布局中的引导程序，以编程方式更新客户端的客户端安装。

### <a name="programatically-update-visual-studio-by-using-the-visual-studio-installer"></a>使用 Visual Studio 安装程序以编程方式更新 Visual Studio

::: moniker range="vs-2017"

可通过以编程方式调用客户端的安装程序并发出 update 命令来启动 Visual Studio 的更新。 例如：

```shell
c:\program files (x86)\microsoft\visual studio\installer\>setup.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2017\Enterprise" 
```

::: moniker-end

::: moniker range=">=vs-2019"

可通过以编程方式调用客户端的安装程序并发出 update 命令来启动 Visual Studio 的更新。 此命令将根据[更新的源位置](/visualstudio/install/update-visual-studio#configure-source-location-of-updates-1)中提供的更新产品来更新 Visual Studio。 如果要更改客户端上的更新源位置，可以通过传入--channelURI 参数以编程方式执行此操作。 例如：  

可以将通道更改为网络布局，并在客户端上执行 update 命令，如下所示：

```shell
c:\program files (x86)\microsoft\visual studio\installer\>setup.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2019\Enterprise" --channelURI "\\\\server\\share\\newlayoutdir\\channelmanifest.json"
```
或类似于这种情况，将更新源设置为 Microsoft 托管位置：

```shell
c:\program files (x86)\microsoft\visual studio\installer\>setup.exe update --installPath "C:\Program Files\Microsoft Visual Studio\2019\Enterprise" --channelURI "https://aka.ms/vs/16/release/channel"
```

::: moniker-end

### <a name="programatically-update-visual-studio-by-using-a-bootstrapper"></a>使用引导程序以编程方式更新 Visual Studio。

::: moniker range=">=vs-2017"

可以通过编程方式从最初安装所用的同一位置调用引导程序来更新 Visual Studio。 源自 Microsoft 托管服务器的所有引导程序均视为来自同一位置。 如果引导程序位于网络布局共享上，则[必须更新网络布局](/visualstudio/install/create-a-network-installation-of-visual-studio#update-or-modify-your-layout)以包含所需的产品更新。

```shell
\\server\share\originalinstallVSdirectory\vs_enterprise.exe update --installPath "C:\clientmachine\installpath" --quiet 
```

::: moniker-end

::: moniker range="vs-2019"

你还可以通过编程方式从其他源位置（包含要将客户端更新到的产品版本）调用引导程序，从而启动 Visual Studio 2019 客户端的更新。 为此，需要在客户端上获取 Visual Studio 2022 安装程序。 若要实现此目的，最简单的方法是[确保新的 Visual Studio 2019 布局使用的是最新安装程序](/visualstudio/install/create-a-network-installation-of-visual-studio#ensure-your-layout-is-using-the-latest-installer)。 如果通过新布局运行引导程序，则客户端上的更新通道将设置为[布局中指定的更新位置](/visualstudio/install/automated-installation-with-response-file)。 例如，可以在客户端计算机上运行以下命令：

::: moniker-end

::: moniker range=">=vs-2022"

还可以通过编程方式从其他源位置（包含要将客户端更新到的产品版本）调用引导程序，从而启动 Visual Studio 客户端的更新。 如果通过新布局运行引导程序，则客户端上的更新通道将设置为[布局中指定的更新位置](/visualstudio/install/automated-installation-with-response-file)。 例如，可以在客户端计算机上运行以下命令：

::: moniker-end

::: moniker range=">=vs-2019"

```shell
   \\server\share\desiredupdatelayoutdir\vs_enterprise.exe update --installPath "C:\clientmachine\installpath" --quiet 
```
无论布局的 response.json 文件中的 channelURI 值为何，都将成为客户端查找未来更新的位置。

::: moniker-end

> [!NOTE]
> 使用 [vswhere.exe 命令](tools-for-managing-visual-studio-instances.md)可标识客户端计算机上 Visual Studio 现有实例的安装路径。

### <a name="programatically-update-a-client-that-doesnt-have-internet-access"></a>以编程方式更新无 Internet 访问的客户端

如果客户端计算机无 Internet 访问，则必须通过网络布局获取更新。 请记住，每当更新 Visual Studio 时，都需要更新两个部分。 第一部分是安装程序，第二部分是 Visual Studio 产品本身。 通过在客户端计算机上运行这些命令，可以指示 Visual Studio 从网络布局显式查找这两个组件 。 第一条命令强制要求安装程序来自布局，第二条命令则阻止在 Internet 上从 Microsoft 托管服务器下载任何包。

 ```shell
    \\server\share\VSlayoutdirectory\vs_enterprise.exe --quiet --update
    \\server\share\VSlayoutdirectory\vs_enterprise.exe update --installPath "C:\clientmachine\installpath" --noWeb --wait --quiet --norestart
 ```
    
确保客户端从网络布局获取更新的另一种方法是在一条命令中将 `--noweb` 和 `--noUpdateInstaller` 选项传递给网络布局上的引导程序。 前者阻止从 Internet 下载更新的工作负载、组件，后者阻止安装程序进行自我更新。 此选项虽然可用，但通常不建议使用，因为应始终使用最新且最合适的安装程序。

> [!IMPORTANT]
> `--noWeb` 选项不会阻止已连接 Internet 的计算机上的 Visual Studio 安装程序检查更新。 而是会阻止客户端下载产品包。 有关详细信息，请参阅[控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)页。

## <a name="get-support-for-your-network-layout"></a>获取对网络布局的支持

如果网络布局遇到问题，请告知我们。 通过[报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)工具（会出现在 Visual Studio 安装程序和 Visual Studio IDE 中）是告知我们的最佳方式。 如果你是 IT 管理员，并且尚未安装 Visual Studio，可以[在此处提交 IT 管理员反馈](https://aka.ms/vs/admin/guide)。 使用此工具时，如果你可以发送 [VS 收集工具的日志](https://aka.ms/vscollect)，这将非常有帮助，可帮助我们诊断和解决问题。

对于安装相关问题，我们还提供[安装聊天](https://visualstudio.microsoft.com/vs/support/#talktous)（仅限英语）支持选项  。

我们还提供其他支持选项。 请参阅我们的 [Visual Studio 开发者社区](https://developercommunity.visualstudio.com/home)。


## <a name="see-also"></a>另请参阅

* [创建和维护网络布局](create-a-network-installation-of-visual-studio.md)
* [Visual Studio 管理员指南](visual-studio-administrator-guide.md)
* [使用命令行参数安装 Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [用于检测和管理 Visual Studio 实例的工具](tools-for-managing-visual-studio-instances.md)
* [控制对基于网络的 Visual Studio 部署的更新](controlling-updates-to-visual-studio-deployments.md)
* [Visual Studio 产品生命周期和维护](/visualstudio/releases/2019/servicing/)
