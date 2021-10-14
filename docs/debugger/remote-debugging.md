---
title: 远程调试 | Microsoft Docs
description: 使用 Visual Studio 远程调试器来调试已部署到另一他计算机上的 Visual Studio 应用程序。
ms.custom:
- remotedebugging
- SEO-VS-2020
ms.date: 09/10/2021
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ddae69c5261b63ef0e62fded1f94de448f82b984
ms.sourcegitcommit: 8fae163333e22a673fd119e1d2da8a1ebfe0e51a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2021
ms.locfileid: "129972383"
---
# <a name="remote-debugging"></a>Remote Debugging
你可以调试已部署在另一台计算机的 Visual Studio 应用程序。 要进行此操作，可使用 Visual Studio 远程调试器。

有关远程调试的深入说明，请参阅以下主题。

|方案|链接|
|-|-|-|
|Azure 应用服务|[远程调试 Azure 上的 ASP.NET](../debugger/remote-debugging-azure.md)，或 Visual Studio Enterprise 的 [Snapshot Debugger](../debugger/debug-live-azure-applications.md)|
|Azure VM|[远程调试 Azure 上的 ASP.NET](../debugger/remote-debugging-azure.md)|
|Azure Service Fabric|[调试 Azure Service Fabric 应用程序](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)|
|ASP.NET|[远程调试 ASP.NET Core](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md) 或[远程调试 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|C# 或 Visual Basic|[远程调试 C# 或 Visual Basic 项目](../debugger/remote-debugging-csharp.md)|
|C++|[远程调试 C++ 项目](../debugger/remote-debugging-cpp.md)|
|通用 Windows 应用 (UWP)|[在远程计算机上运行 UWP 应用](../debugger/run-windows-store-apps-on-a-remote-machine.md)或[调试安装的应用包](../debugger/debug-installed-app-package.md)|

如果只想下载并安装远程调试器，且不需要针对方案的任何其他说明，请按照本文中的步骤进行操作。

## <a name="download-and-install-the-remote-tools"></a>下载和安装远程工具

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="requirements"></a><a name="requirements_msvsmon"></a> 要求

[!INCLUDE [remote-debugger-requirements](../debugger/includes/remote-debugger-requirements.md)]

## <a name="optional-to-run-the-remote-debugger-from-a-file-share"></a><a name="fileshare_msvsmon"></a>（可选）从文件共享运行远程调试器

可以在已安装 Visual Studio Community、Professional 或 Enterprise 的计算机上找到远程调试器 (msvsmon.exe)。 在某些方案中，设置远程调试的最简便方法是从文件共享运行远程调试器 (msvsmon.exe)。 有关使用限制，请参阅远程调试器的“帮助”页（远程调试器中的“帮助”>“使用情况”）。

1. 在与你的 Visual Studio 版本匹配的目录中找到 msvsmon.exe：

   ::: moniker range=">=vs-2022"

   Program Files\Microsoft Visual Studio\2022\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe

   Program Files\Microsoft Visual Studio\2022\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe

   ::: moniker-end
   ::: moniker range="vs-2019"

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   *Program Files (x86)\Microsoft Visual Studio\2019\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   ::: moniker-end
   ::: moniker range="vs-2017"

   *程序文件 (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x86\msvsmon.exe*

   *程序文件 (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Remote Debugger\x64\msvsmon.exe*

   ::: moniker-end

2. 在 Visual Studio 计算机上共享“Remote Debugger”文件夹。

3. 在远程计算机上，从共享文件夹运行 msvsmon.exe。 请按照[设置说明](#bkmk_setup)操作。

> [!TIP]
> 有关命令行安装和命令行参考，请参阅 msvsmon.exe 的“帮助”页，方法是在安装了 Visual Studio 的计算机上的命令行中键入 ``msvsmon.exe /?``（或转到远程调试器中的“帮助”>“使用情况”）。

## <a name="set-up-the-remote-debugger"></a><a name="bkmk_setup"></a>设置远程调试器

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

### <a name="configure-the-remote-debugger"></a><a name="configure_msvsmon"></a>配置远程调试器
首次启动后，你可以更改远程调试器的部分配置。

- 如果需要为其他用户添加权限以连接到远程调试器，请选择“工具”>“权限”。 你必须拥有管理员特权才能授予或拒绝权限。

     > [!IMPORTANT]
     > 可以在其他用户帐户（不同于你在 Visual Studio 计算机上使用的用户帐户）下运行远程调试器，但你必须将该用户帐户添加到远程调试器权限中。

     或者，你可以从具有 /allow \<username> 参数的命令行启动远程调试器：msvsmon /allow \<username@computer> 。

- 如果需要为远程工具更改身份验证模式或端口号，或指定超时值：选择“工具”>“选项”。

     有关默认使用的端口号的列表，请参阅[远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)。

     > [!WARNING]
     > 可以选择在“无身份验证”模式下运行远程工具，但强烈建议不要使用此模式。 在此模式下运行时，无法保证网络安全。 只有在确认网络不会遇到恶意通信的情况下，才可选择“无身份验证”模式。

## <a name="optional-configure-the-remote-debugger-as-a-service"></a><a name="bkmk_configureService"></a>（可选）将远程调试器配置为服务
对于在 ASP.NET 和其他服务器环境中调试，你必须以管理员身份运行远程调试器；或者，如果你希望它始终运行，则将远程调试器作为服务运行。

 如果要将远程调试器配置为服务，请执行以下步骤。

1. 找到  “远程调试器配置向导”(rdbgwiz.exe)。 （这是独立于远程调试器的应用程序。）仅在你安装远程工具后，它才可用。 它不与 Visual Studio 一起安装。

2. 开始运行配置向导。 当第一页出现时，单击“下一步” 。

3. 勾选“将 Visual Studio 2015 远程调试器作为服务运行”  复选框。

4. 添加用户帐户的名称和密码。

    可能需要在“开始”页或窗口（查找“本地安全策略”[secpol.msc]）（或在命令提示符处键入 secpol）向此帐户添加“作为服务登录”用户权限。 当显示窗口时，双击“用户权限分配” ，然后在右窗格中找到  “作为服务登录”。 双击该选项。 将用户帐户添加到“属性”窗口，然后点击“确定”） 。 单击 **“下一步”** 。

5. 选择你希望远程工具与之通信的网络类型。 必须至少选择一种网络类型。 如果这些计算机通过域连接，则应选择第一项。 如果这些计算机通过工作组或家庭组连接，则应选择第二或第三项。 单击 **“下一步”** 。

6. 如果可以启动服务，则会显示 “你已成功完成 Visual Studio 远程调试器配置向导”。 如果无法启动服务，则会显示“未能完成 Visual Studio 远程调试器配置向导” 。 此页还提供了为使服务正常启动要遵循的一些提示。

7. 单击 **“完成”** 。

   此时，远程调试器正作为服务运行。 可以通过转到“控制面板”>“服务”并找到 “Visual Studio 2015 远程调试器”来对此进行验证 。

   可以从“控制面板”>“服务”停止和启动远程调试器服务。

## <a name="set-up-debugging-with-remote-symbols"></a>使用远程符号设置调试

[!INCLUDE [remote-debugger-symbols](../debugger/includes/remote-debugger-symbols.md)]

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [配置 Windows 防火墙以便进行远程调试](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [远程调试器端口分配](../debugger/remote-debugger-port-assignments.md)
- [远程调试远程 IIS 计算机上的 ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)
- [远程调试错误和疑难解答](../debugger/remote-debugging-errors-and-troubleshooting.md)