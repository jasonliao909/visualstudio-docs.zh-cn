---
description: 当你尝试调试在 Web 服务器上运行的 ASP.NET 应用程序时，可能会收到此错误消息：无法在 Web 服务器上启动调试。
title: 无法在 Web 服务器上启动调试 | Microsoft Docs
ms.date: 05/23/2018
ms.topic: error-reference
f1_keywords:
- vs.debug.error.http
- vwd.nonadmin.error.
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- IIS, debugging DLLs
- debugger, Web application errors
- unable to start debugging error
- security [debugger], Web applications
- debugging [Visual Studio], errors
- HTTP servers, debugging error
- security settings, checking for default Web sites
- errors [debugger], unable to start debugging
- debugging ASP.NET Web applications, unable to start debugging error
- remote debugging, errors
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f3326bf39a43e0bf065e0a0b76288f915705d07c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122134033"
---
# <a name="error-unable-to-start-debugging-on-the-web-server"></a>错误：无法在 Web 服务器上启动调试

当尝试对在 Web 服务器上运行的 ASP.NET 应用程序进行调试时，可能会得到此错误信息：`Unable to start debugging on the Web server`。

通常情况下，由于错误或配置发生更改，需要更新应用程序池和 / 或 IIS 重置，因此会出现此错误。 可通过打开命令提示符并键入 `iisreset` 重置 IIS。

## <a name="what-is-the-detailed-error-message"></a><a name="specificerrors"></a>详细的错误消息是什么？

`Unable to start debugging on the Web server`是通用消息。 通常情况下，更具体的消息包含在错误字符串，也许能够帮助你确定问题或搜索更精确的修补程序的原因。 下面是几个附加到主错误消息的更常见的错误消息：

- [IIS 未列出与启动 URL 匹配的网站](#IISlist)
- [Web 服务器配置不正确](#web_server_config)
- [无法连接到 Web 服务器](#unabletoconnect)
- [Web 服务器未及时响应](#webservertimeout)
- [Microsoft Visual Studio 远程调试监视器 (msvsmon.exe) 似乎没有在远程计算机上运行](#msvsmon)
- [远程服务器返回了错误](#server_error)
- [无法启动 ASP.NET 调试](#aspnet)
- [调试器无法连接到远程计算机](#cannot_connect)
- [请参见有关常见配置错误的帮助。在调试器外部运行网页可能会提供进一步的信息。](#see_help)
- [不支持此操作。未知错误：错误号](#operation_not_supported)

## <a name="iis-does-not-list-a-website-that-matches-the-launch-url"></a><a name="IISlist"></a> IIS 未列出与启动 URL 匹配的网站

- 以管理员身份重新启动 Visual Studio ，然后重试调试。 （某些 ASP.NET 调试方案需要提升权限。）

    若要将 Visual Studio 配置为始终以管理员身份运行，请右键单击 Visual Studio 快捷方式图标，选择“属性”>“高级”，然后选择“始终以管理员身份运行”。

## <a name="the-web-server-is-not-configured-correctly"></a><a name="web_server_config"></a> Web 服务器配置不正确

- 请参阅支持论坛上的[错误：Web 服务器配置不正确](../debugger/error-the-web-server-is-not-configured-correctly.md)。

## <a name="unable-to-connect-to-the-webserver"></a><a name="unabletoconnect"></a> 无法连接到 Web 服务器

- 是否在同一台计算机上运行 Visual Studio 和 Web 服务器，并使用 **F5** (而不是 **附加到进程**)进入调试？ 打开项目属性，并确保将项目配置为连接到正确的 Web 服务器并启动 URL。 (打开 **属性 > Web > 服务器** 或 **属性 > 调试** 具体取决于你的项目类型。 对于 Web 窗体项目，打开 **属性页 > 启动选项 > 服务器**。)

- 否则，请重新启动应用程序池，然后重置 IIS。 有关详细信息，请参阅[检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。

## <a name="the-web-server-did-not-respond-in-a-timely-manner"></a><a name="webservertimeout"></a> Web 服务器未及时响应

- 重置 IIS，然后再次尝试进行调试。 可以将多个调试器实例附加到 IIS 进程；重置操作将终止这些实例。 有关详细信息，请参阅[检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。

## <a name="the-microsoft-visual-studio-remote-debugging-monitormsvsmonexe-does-not-appear-to-be-running-on-the-remote-computer"></a><a name="msvsmon"></a> Microsoft Visual Studio 远程调试监视器 (msvsmon.exe) 似乎没有在远程计算机上运行

- 如果在远程计算机上进行调试，请确保[已安装并且正在运行远程调试器](../debugger/remote-debugging.md)。 如果消息提到了防火墙，请确保[防火墙中正确的端口](../debugger/remote-debugger-port-assignments.md)处于打开状态，尤其是在使用第三方防火墙时。
- 如果使用的是 HOSTS 文件，请确保其配置正确。 例如，如果是按 F5 进行调试（而不是“附加到进程”），则 HOSTS 文件中需要包含与项目属性中相同的项目 URL，“属性”>“Web”>“服务器”或“属性”>“调试”，具体取决于项目类型   。

## <a name="the-remote-server-returned-an-error"></a><a name="server_error"></a> 远程服务器返回了错误

检查[IIS 日志文件](https://support.microsoft.com/help/943891/the-http-status-code-in-iis-7-0--iis-7-5--and-iis-8-0)错误子代码和其他信息，以及此 IIS 7[博客文章](https://blogs.iis.net/tomkmvp/troubleshoot-a-403)。

此外，下面是一些常见的错误代码和一些建议。
- (403) 已禁止。 此错误有许多可能的原因，因此请检查您的日志文件和网站的 IIS 安全设置。 请确保服务器的 web.config 包含`debug=true`编译元素中。 请确保你的 Web 应用程序文件夹有正确的权限并验证你的应用程序池配置正确 （密码可能已更改）。 请参阅[检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。 如果这些设置是否已正确和本地调试，还验证连接到正确的服务器类型和 URL (在 **属性 > Web > 服务器** 或 **属性 > 调试**，具体取决于你的项目类型）。
- (503) 服务器不可用。 应用程序池可能由于错误或配置更改而停止。 重启应用程序池。
- (404) 未找到。 请确保应用程序池是针对正确的 ASP.NET 版本配置的。

## <a name="could-not-start-aspnet-debugging"></a><a name="aspnet"></a> 无法启动 ASP.NET 调试

- 重启应用程序池并重置 IIS。 有关详细信息，请参阅[检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。
- 如果正在 URL 重写，测试一个基本 web.config，没有 URL 重写的配置。 请参阅 **注意** 有关 URL 重写中的模块 [检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。

## <a name="the-debugger-cannot-connect-to-the-remote-computer"></a><a name="cannot_connect"></a> 调试器无法连接到远程计算机

若要在本地进行调试，请在 Visual Studio 中打开项目属性，并确保将项目配置为连接到正确的 Web 服务器和 URL。 (打开 **属性 > Web > 服务器** 或 **属性 > 调试** 具体取决于您的项目类型。)

进行本地调试时可能发生此错误，因为 Visual Studio 是一个 32 位应用程序中，需要使用 64 位版远程调试器来调试 64 位应用程序。 检查 IIS 上的应用程序池，确保“启用 32 位应用程序”设置为 `true`，重启 IIS 然后重试。

此外，如果你使用HOSTS文件，请确保配置正确。 例如，HOSTS文件中必须包含相同的项目 URL 在项目属性中，**属性 > Web > 服务器** 或 **属性 > 调试**，具体取决于项目类型。

## <a name="see-help-for-common-configuration-errors-running-the-webpage-outside-of-the-debugger-may-provide-further-information"></a><a name="see_help"></a> 请参见有关常见配置错误的帮助。 在调试器外部运行网页可能会提供进一步的信息。

- 是否在同一台计算机上运行 Visual Studio 和 Web 服务器？ 打开项目属性，并确保将项目配置为连接到正确的 Web 服务器并启动 URL。 (打开 **属性 > Web > 服务器** 或 **属性 > 调试** 具体取决于您的项目类型。)

- 如果这不起作用，或者你正在进行远程调试，请按照[检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)中的步骤操作。

## <a name="operation-not-supported-unknown-error-errornumber"></a><a name="operation_not_supported"></a> 不支持此操作。 未知错误：错误号

如果正在 URL 重写，测试一个基本 web.config，没有 URL 重写的配置。 请参阅 **注意** 有关 URL 重写中的模块 [检查 IIS 配置](#vxtbshttpservererrorsthingstocheck)。

## <a name="check-your-iis-configuration"></a><a name="vxtbshttpservererrorsthingstocheck"></a> 检查 IIS 配置

在详细介绍了解决问题的步骤之后，在再次尝试调试前，你可能还需要重置 IIS。 你可以通过打开命令提示符并键入 `iisreset` 执行该操作。

* 停止并重启 IIS 应用程序池，然后重试。

    应用程序池可能由于出现错误而停止。 或者，你所做的另一种配置更改可能要求停止并重启应用程序池。

    > [!NOTE]
    > 如果应用程序池保持停止，你可能需要从控制面板卸载 URL 重写模块。 你也可以使用 Web 平台安装程序 (WebPI) 重新安装它。 大量的系统升级后可能出现此问题。

* 请检查您的应用程序池配置，如果需要就进行更正，然后重试。

    可能 Visual Studio 项目版本不匹配 ASP.NET 配置的应用程序池。 更新应用程序池中的 ASP.NET 版本并重新启动它。 有关详细信息，请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)。

    此外，如果密码凭据已更改，可能需要在应用程序池或网站中进行更新。  可在应用程序池中的“高级设置”>“进程模型”>“身份”中更新这些凭据。 对于网站，请在“基础设置”>“连接方式…”中更新这些凭据。重启应用程序池。

* 检查 Web 应用程序文件夹是否具有适当的权限。

    请确保你提供 IIS_IUSRS、IUSR、或与特定用户关联[应用程序池](/iis/manage/configuring-security/application-pool-identities)读取和执行的 Web 应用程序文件夹的权限。 修复该问题并重新启动应用程序池。

* 请确保在 IIS 上安装了正确版本的 ASP.NET。

    IIS 中的ASP.NET 与 Visual Studio 项目的版本不匹配可能会导致此问题。 可能需要在 web.config 中设置框架版本。若要在 IIS 上安装 ASP.NET，请使用 [Web 平台安装程序 (WebPI)](https://www.microsoft.com/web/downloads/platform.aspx)。 另请参阅[IIS 8.0 使用 ASP.NET 3.5 和 ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)或为 ASP.NET Core [使用 IIS 的 Windows 上的主机](https://docs.asp.net/en/latest/publishing/iis.html)。

* 如果只使用 IP 地址，则解决身份验证错误

     默认情况下，IP 地址被假定为 Internet 的一部分，而在 Internet 上不进行 NTLM 身份验证。 如果已在 IIS 中将网站配置为需要身份验证，则此身份验证将失败。 若要更正此问题，可以指定远程计算机的名称，而不是 IP 地址。

## <a name="other-causes"></a>其他原因

如果此问题与 IIS 配置无关，请尝试以下步骤：

- 通过管理员权限重启 Visual Studio，然后重试。

    例如，使用 Web 部署一些需要提升 Visual Studio 权限的 ASP.NET 调试方案。

- 如果正在运行 Visual Studio 多个实例，（使用管理员权限）重新打开你的 Visual Studio 一个实例中的项目，然后重试。

- 如果使用的是具有本地地址的 HOSTS 文件，请尝试使用环回地址，而不是计算机的 IP 地址。

    如果不使用本地地址，请确保 HOSTS 文件包含与项目属性中相同的项目 URL，“属性”>“Web”>“服务器”或“属性”>“调试”，具体取决于项目类型 。

## <a name="more-troubleshooting-steps"></a>更多疑难解答步骤

* 在服务器上的浏览器中打开 localhost 页。

     如果未正确安装 IIS，则当你在浏览器中键入 `http://localhost` 时会收到错误。

     若要详细了解如何部署到 IIS，请参阅[使用 ASP.NET 3.5 和 ASP.NET 4.5 的IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)，或者[使用 IIS 在 Windows 上托管 ASP.NET Core](https://docs.asp.net/en/latest/publishing/iis.html)。

* 在服务器上创建基本 ASP.NET 应用程序（或使用基本 web.config 文件）。

    如果无法让应用使用调试器，请尝试在服务器上本地创建基本 ASP.NET 应用程序，并尝试对其进行调试。 （可能需要使用默认的 ASP.NET MVC 模板。）如果可以调试该基本应用，这也许能帮助你识别两种配置的不同之处。 查看 web.config 文件中的设置差异，例如 URL 重写规则。

## <a name="see-also"></a>请参阅
- [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)
