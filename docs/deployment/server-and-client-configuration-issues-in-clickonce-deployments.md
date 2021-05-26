---
title: 'ClickOnce 服务 (/客户端配置) '
description: 了解可能影响 ClickOnce 应用程序的部署的服务器和客户端配置问题。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
- Windows applications, ClickOnce deployments
ms.assetid: 929e5fcc-dd56-409c-bb57-00bd9549b20b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 8040fb8028666d0dd551369b6b7f782de09058ca
ms.sourcegitcommit: 18e7300d4878f2fcd0263a4aff31a755ae8fc289
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "110449937"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 部署中的服务器和客户端配置问题
如果在 Windows Server Internet Information Services (IIS) ，并且部署包含 Windows 无法识别的文件类型（如 Microsoft Word 文件）时，IIS 将拒绝传输该文件，并且部署不会成功。

 此外，某些 Web 服务器和 Web 应用程序软件（如 ）包含无法下载的文件 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 和文件类型的列表。 例如， [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 阻止下载所有Web.config文件。  这些文件可能包含敏感信息，例如用户名和密码。

 尽管此限制不会导致下载核心文件（如清单和程序集）出现问题，但此限制可能会阻止下载作为应用程序一部分包含 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 数据文件。 在 中，可以通过删除禁止从 IIS 配置管理器下载此类文件的处理程序来解决 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 此错误。 有关更多详细信息，请参阅 IIS 服务器文档。

 某些 Web 服务器可能会阻止扩展名为 *.dll、.config* 和 *.mdf 的文件*。  基于 Windows 的应用程序通常包含具有其中一些扩展名的文件。 如果用户尝试运行访问 Web 服务器上阻止的文件的应用程序，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 会导致错误。 默认情况下，使用 .deploy 文件扩展名发布每个应用程序文件，而不是取消 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 阻止所有文件扩展名。 因此，管理员只需配置 Web 服务器以取消阻止以下三个文件扩展名：

- *.application*

- *.manifest*

- *.deploy*

  但是，可以通过清除"发布选项"对话框中的"使用 **.deploy"** 文件扩展名选项来 [](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100))禁用此选项，在这种情况下，必须将 Web 服务器配置为取消阻止应用程序中使用的所有文件扩展名。

  例如，如果使用的是未安装 .NET Framework 的 IIS，或者使用的是其他 Web 服务器 (例如 Apache) ，则必须配置 *.manifest*、 *. application* 和 *.deploy。*

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce 和安全套接字层 (SSL) 
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序将在 ssl 上正常运行，但 Internet Explorer 会引发有关 ssl 证书的提示。 当证书出现问题时，可能会引发提示，例如，当站点名称不匹配或证书已过期时。 若要 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 通过 SSL 连接进行操作，请确保证书是最新的，并且证书数据与站点数据匹配。

## <a name="clickonce-and-proxy-authentication"></a>ClickOnce 和代理身份验证
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 .NET Framework 3.5 开始，为 Windows 集成的代理身份验证提供支持。 不需要特定的 machine.config 指令。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不提供对其他身份验证协议（如基本或摘要）的支持。

 你还可以将修补程序应用到 .NET Framework 2.0 来启用此功能。 有关详细信息，请参阅 [修复：尝试将在 .NET Framework 2.0 中创建的 ClickOnce 应用程序安装到配置为使用代理服务器的客户端计算机时，请参阅修复：错误消息： "需要代理身份验证"](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)。

 有关详细信息，请参阅[ \<defaultProxy> 网元 (网络设置) ](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)。

## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce 和 Web 浏览器兼容性
 目前， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 只有在使用 Internet Explorer 打开部署清单的 URL 时，安装才会启动。 只有在将 Internet Explorer 设置为默认 Web 浏览器的情况下，从其他应用程序（例如 Microsoft Office Outlook）启动其 URL 的部署才会成功启动。

> [!NOTE]
> 如果部署提供程序不为空或者已安装 Microsoft .NET Framework 助手扩展，则支持 Mozilla Firefox。 此扩展与 .NET Framework 3.5 SP1 一起打包。 对于 XBAP 支持，NPWPF 插件将在需要时激活。

## <a name="activate-clickonce-applications-through-browser-scripting"></a>通过浏览器脚本激活 ClickOnce 应用程序
 如果已开发使用活动脚本启动应用程序的自定义网页，可能会发现该应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不会在某些计算机上启动。 Internet Explorer包含名为"自动 **提示文件** 下载"的设置，这会影响此行为。 此设置在其"选项"菜单中的"**安全"选项卡****上可用**，这会影响此行为。 它称为 **"自动提示文件下载"，** 并列在"下载 **"类别** 下。 默认情况下， 属性设置为 **Intranet** 网页的"启用"，对于Internet 网页，设置为"默认禁用"。 当此设置设置为"禁用"时，将阻止以编程方式激活应用程序 (例如，通过将其 URL 分配给属性) [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `document.location` 应用程序。 在这种情况下，用户只能通过用户启动的下载来启动应用程序，例如，单击设置为应用程序 URL 的超链接。

## <a name="additional-server-configuration-issues"></a>其他服务器配置问题

##### <a name="administrator-permissions-required"></a>所需的管理员权限
 如果要使用 HTTP 发布，则必须在目标服务器上具有管理员权限。 IIS 需要此权限级别。 如果不使用 HTTP 进行发布，则只需对目标路径具有写入权限。

##### <a name="server-authentication-issues"></a>服务器身份验证问题
 发布到已关闭"匿名访问"的远程服务器时，将收到以下警告：

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> 如果站点提示输入非默认凭据的凭据，则 NTLM (NT 质询响应) 身份验证有效;如果想保存提供的凭据供将来会话使用，请在安全对话框中单击"确定"。 但是，此解决方法将不能用于基本身份验证。

## <a name="use-third-party-web-servers"></a>使用第三方 Web 服务器
 如果要 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 IIS 之外的 Web 服务器部署应用程序，则如果服务器返回密钥文件的不正确内容类型（ [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 如部署清单和应用程序清单），则可能会遇到问题。 若要解决此问题，请参阅 Web 服务器的帮助文档，了解如何向服务器添加新内容类型，并确保下表中列出的所有文件扩展名映射都已准备就绪。

|文件扩展名|内容类型|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce 和映射驱动器
 如果使用 Visual Studio 发布 ClickOnce 应用程序，则不能将映射驱动器指定为安装位置。 不过，你可以通过使用清单生成器和编辑器 (Mage.exe 和 MageUI.exe) ，将 ClickOnce 应用程序修改为从映射驱动器安装。 有关详细信息，请参阅[Mage.exe （清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)并[MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)。

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>用于安装应用程序的 FTP 协议不受支持
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 支持从任何 HTTP 1.1 Web 服务器或文件服务器安装应用程序。 安装应用程序不支持 FTP、文件传输协议。 仅可使用 FTP 发布应用程序。 下表总结了这些差异：

| URL 类型 | 说明 |
|----------| - |
| ftp:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议发布应用程序。 |
| http:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |
| https:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |
| file:// | 您可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用此协议安装应用程序。 |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2： Windows 防火墙
 默认情况下，Windows XP SP2 启用 Windows 防火墙。 如果要在安装了 Windows XP 的计算机上开发应用程序，仍可以 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从运行 IIS 的本地服务器发布和运行应用程序。 但是，除非打开 Windows 防火墙，否则不能从另一台计算机访问运行 IIS 的服务器。 有关管理 Windows 防火墙的说明，请参阅 Windows 帮助。

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server：启用 FrontPage 服务器扩展
 FrontPage 服务器扩展将应用程序发布到使用 HTTP 的 Windows Web 服务器时，需要 Microsoft 提供证书。

 默认情况下，Windows Server 未安装FrontPage 服务器扩展。 如果要使用 发布到使用 HTTP 和 FrontPage 服务器扩展 的 Windows Server Web 服务器，必须先 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] FrontPage 服务器扩展服务器。 可以使用 Windows Server 中的管理服务器管理工具执行安装。

## <a name="windows-server-locked-down-content-types"></a>Windows Server：锁定的内容类型
 除某些已知内容类型（例如 [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] .htm、.html、.txt等） (外，IIS 会锁定所有) 。 若要使用此服务器启用应用程序的部署，需要更改 IIS 设置，以允许下载应用程序使用的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] *.application* *、.manifest* 和任何其他自定义文件类型的文件。

 如果使用 IIS 服务器进行部署，请inetmgr.exe为默认网页添加新的文件类型：

- 对于 *.application 和* *.manifest* 扩展，MIME 类型应为"application/x-ms-application"。 对于其他文件类型，MIME 类型应为"application/octet-stream"。

- 如果创建扩展名为""且 MIME 类型为 \<em> "application/octet-stream"的 MIME 类型，则允许下载未阻止文件类型的文件。  (但是，无法下载阻止的文件类型，如 *\* .aspx* 和 *\* .asmx。)*

  有关在 Windows Server 上配置 MIME 类型的特定说明，请参阅如何将 MIME 类型添加到 [网站或应用程序](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)。

## <a name="content-type-mappings"></a>内容类型映射
 通过 HTTP 发布时， (*.application*) 的 MIME 类型类型应为"application/x-ms-application"。 如果在服务器上.NET Framework 2.0，则会自动进行设置。 如果未安装，则需要为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序 vroot (或整个服务器) 创建 MIME 类型关联。

 如果使用 IIS 服务器进行部署，请运行 <em>inetmgr。</em>exe，并为 *应用程序* 扩展添加新的 "应用程序/x 应用程序" 内容类型。

## <a name="http-compression-issues"></a>HTTP 压缩问题
 利用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，你可以执行使用 HTTP 压缩的下载，这是使用 GZIP 算法在将流发送到客户端之前压缩数据流的 Web 服务器技术。 在此示例中，客户端（在此示例中）将在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 读取文件之前对其进行解压缩。

 如果使用的是 IIS，则可以轻松启用 HTTP 压缩。 但是，当启用 HTTP 压缩时，仅对某些文件类型（即 HTML 和文本文件）启用它。 若要为程序 *集 ()* 、xml (*xml*) 、部署 *清单 ()  (和* 应用 *程序清单启用* 压缩，则必须将这些文件类型添加到要压缩的 IIS 类型列表中。 将文件类型添加到部署之前，只会压缩文本和 HTML 文件。

 有关 IIS 的详细说明，请参阅 [如何为 HTTP 压缩指定其他文档类型](/troubleshoot/iis/content-types-http-compression.md)。

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
