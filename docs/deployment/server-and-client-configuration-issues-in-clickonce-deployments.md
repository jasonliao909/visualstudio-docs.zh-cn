---
title: 服务器/客户端配置问题 (ClickOnce)
description: 了解可能影响 ClickOnce 应用程序部署的服务器和客户端配置问题。
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
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 3ae02ecb906c14992672c822a7bda1c579d91d43
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665461"
---
# <a name="server-and-client-configuration-issues-in-clickonce-deployments"></a>ClickOnce 部署中的服务器和客户端配置问题
如果在 Windows Server 上使用 Internet Information Services (IIS)，并且部署包含 Windows 无法识别的文件类型（例如 Microsoft Word 文件），则 IIS 将拒绝传输该文件，并且部署不会成功。

 此外，某些 Web 服务器和 Web 应用程序软件（如 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)]）包含无法下载的文件和文件类型的列表。 例如，[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 阻止下载所有 Web.config 文件。 这些文件可能包含敏感信息，例如用户名和密码。

 虽然此限制不会对下载核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 文件（如清单和程序集）造成任何问题，但此限制可能会阻止你下载作为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的一部分包含的数据文件。 在 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 中，可以通过删除禁止从 IIS 配置管理器下载此类文件的处理程序来解决此错误。 有关更多详细信息，请参阅 IIS 服务器文档。

 某些 Web 服务器可能会阻止扩展名为 .dll、.config 和 .mdf 的文件  。 基于 Windows 的应用程序通常包含具有其中一些扩展名的文件。 如果用户尝试运行访问 Web 服务器上阻止的文件的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，则会导致错误。 默认情况下，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不是取消阻止所有文件扩展名，而是发布具有 .deploy 文件扩展名的每个应用程序文件。 因此，管理员只需配置 Web 服务器以取消阻止以下三个文件扩展名：

- *.application*

- *.manifest*

- *.deploy*

  但是，你可以通过清除[“发布选项”对话框](/previous-versions/visualstudio/visual-studio-2010/7z83t16a(v=vs.100))上的“使用 ".deploy" 文件扩展名”选项来禁用此选项，在这种情况下，必须配置 Web 服务器以取消阻止应用程序中使用的所有文件扩展名。

  例如，如果在未安装 .NET Framework 的地方使用 IIS，或者如果正在使用其他 Web 服务器（例如 Apache），则必须配置 .manifest、.application 和 .deploy  。

## <a name="clickonce-and-secure-sockets-layer-ssl"></a>ClickOnce 和安全套接字层 (SSL)
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以正常使用 SSL，除非 Internet Explorer 提示 SSL 证书。 当证书出现问题（例如站点名称不匹配或证书已过期）时，可能会引发提示。 要使 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 通过 SSL 连接工作，请确保证书是最新的，并且证书数据与站点数据相匹配。

## <a name="clickonce-and-proxy-authentication"></a>ClickOnce 和代理身份验证
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 从 .NET Framework 3.5 开始为 Windows 集成代理身份验证提供支持。 不需要特定 machine.config 指令。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 不支持其他身份验证协议，例如 Basic 或 Digest。

 你还可以将修补程序应用于 .NET Framework 2.0 以启用此功能。 有关详细信息，请参阅[修复：尝试将在 .NET Framework 2.0 中创建的 ClickOnce 应用程序安装到配置为使用代理服务器的客户端计算机上时，会出现错误消息：“需要代理身份验证”](https://support.microsoft.com/help/917952/fix-error-message-when-you-try-to-install-a-clickonce-application-that)。

 有关详细信息，请参阅 [\<defaultProxy> 元素（网络设置）](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings)。

## <a name="clickonce-and-web-browser-compatibility"></a>ClickOnce 和 Web 浏览器兼容性
 目前，只有在使用 Internet Explorer 打开部署清单的 URL 时，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装才启动。 只有当 Internet Explorer 设置为默认 Web 浏览器时，其 URL 从另一个应用程序（如 Microsoft Office Outlook）启动的部署才会成功启动。

> [!NOTE]
> 如果部署提供程序不为空或安装了 Microsoft .NET Framework 助手扩展，则支持 Mozilla Firefox。 此扩展与 .NET Framework 3.5 SP1 一起打包。 对于 XBAP 支持，NPWPF 插件将根据需要激活。

## <a name="activate-clickonce-applications-through-browser-scripting"></a>通过浏览器脚本激活 ClickOnce 应用程序
 如果已开发使用活动脚本启动 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的自定义网页，可能会发现该应用程序不会在某些计算机上启动。 Internet Explorer 包含一个称为“自动提示文件下载”的设置，这会影响此行为。 此设置可在其影响此行为的“选择”菜单中的“安全”选项卡上找到 。 它被称为“自动提示文件下载”，列在“下载”类别下 。 默认情况下，此属性针对 Intranet 网页设置为“启用”，针对 Internet 网页设置为“禁用” 。 此设置设置为“禁用”时，任何以程序方式激活 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的尝试（例如，通过将其 URL 分配给 `document.location` 属性）都将被阻止。 在这种情况下，用户只能通过用户启动的下载来启动应用程序，例如，单击设置为应用程序 URL 的超链接。

## <a name="additional-server-configuration-issues"></a>其他服务器配置问题

##### <a name="administrator-permissions-required"></a>需要管理员权限
 如果要使用 HTTP 发布，则必须在目标服务器上具有管理员权限。 IIS 需要此权限级别。 如果不使用 HTTP 进行发布，则只需对目标路径具有写入权限。

##### <a name="server-authentication-issues"></a>服务器身份验证
 发布到已关闭“匿名访问”的远程服务器时，将收到以下警告：

```
"The files could not be downloaded from http://<remoteserver>/<myapplication>/.  The remote server returned an error: (401) Unauthorized."
```

> [!NOTE]
> 如果站点提示默认凭据以外的凭据，你可以进行 NTLM（NT 质询-响应）身份验证工作，并在安全对话框中，如果想要为以后的会话保存所提供的凭据，请在出现提示时单击“确定”。 但是，此解决方法将不能用于基本身份验证。

## <a name="use-third-party-web-servers"></a>使用第三方 Web 服务器
 在从 IIS 以外的 Web 服务器部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时，如果服务器返回关键 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 文件（如部署清单和应用程序清单）的不正确内容类型，则可能会遇到问题。 若要解决这个问题，请参阅 Web 服务器的帮助文档，了解如何向服务器添加新内容类型，并确保下表中列出的所有文件名扩展映射都已到位。

|文件扩展名|内容类型|
|-------------------------|------------------|
|`.application`|`application/x-ms-application`|
|`.manifest`|`application/x-ms-manifest`|
|`.deploy`|`application/octet-stream`|
|`.msu`|`application/octet-stream`|
|`.msp`|`application/octet-stream`|

## <a name="clickonce-and-mapped-drives"></a>ClickOnce 和映射驱动器
 如果使用 Visual Studio 发布 ClickOnce 应用程序，则不能将映射驱动器指定为安装位置。 但是，可使用清单生成器和编辑器（Mage.exe 和 MageUI.exe）修改 ClickOnce 应用程序以从映射驱动器进行安装。 有关详细信息，请参阅[Mage.exe （清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)并[MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)。

## <a name="ftp-protocol-not-supported-for-installing-applications"></a>FTP 协议不支持安装应用程序
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 支持从任何 HTTP 1.1 Web 服务器或文件服务器安装应用程序。 FTP（文件传输协议）不支持安装应用程序。 只能使用 FTP 发布应用程序。 下表对这些差异进行了汇总：

| URL 类型 | 说明 |
|----------| - |
| ftp:// | 可使用此协议发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 |
| http:// | 可使用此协议安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 |
| https:// | 可使用此协议安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 |
| file:// | 可使用此协议安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 |

## <a name="windows-xp-sp2-windows-firewall"></a>Windows XP SP2：Windows 防火墙
 默认情况下，Windows XP SP2 启用 Windows 防火墙。 如果在安装了 WINDOWS XP 的计算机上开发应用程序，仍可从运行 IIS 的本地服务器发布和运行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 但是，无法从另一台计算机访问运行 IIS 的服务器，除非打开 Windows 防火墙。 有关管理 Windows 防火墙的说明，请参阅 Windows 帮助。

## <a name="windows-server-enable-frontpage-server-extensions"></a>Windows Server：启用 FrontPage 服务器扩展
 将应用程序发布到使用 HTTP 的 Windows Web 服务器时，需要 Microsoft 的 FrontPage 服务器扩展。

 默认情况下，Windows Server 未安装 FrontPage 服务器扩展。 如果要使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 发布到使用 HTTP 和 FrontPage 服务器扩展的 Windows Server Web 服务，必须先安装 FrontPage 服务器扩展。 可使用 Windows Server 中的管理服务器管理工具来执行安装。

## <a name="windows-server-locked-down-content-types"></a>Windows Server：锁定的内容类型
 [!INCLUDE[WinXPSvr](../debugger/includes/winxpsvr_md.md)] 上的 IIS 锁定了除某些已知内容类型（例如 .htm、.html、.txt 等）之外的所有文件类型  。 若要使用此服务器部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，则需要更改 IIS 设置，以便下载应用程序使用的类型 .application、.manifest 和任何其他自定义文件类型的文件 。

 如果使用 IIS 服务器进行部署，请运行 inetmgr.exe 并为默认网页添加新的文件类型：

- 对于 .application 和 .manifest 扩展名，MIME 类型应为“application/x-ms-application” 。 对于其他文件类型，MIME 类型应为“application/octet-stream”。

- 如果创建扩展名为“\<em>”且 MIME 类型为“application/octet-stream”的 MIME 类型，则允许下载未阻止文件类型的文件。 （但是，无法下载 \*.aspx 和 \*.asmx 等被阻止的文件类型 。）

  有关在 Windows Server 上配置 MIME 类型的特定说明，请参阅[如何将 MIME 类型添加到网站或应用程序](/iis/configuration/system.webserver/staticcontent/mimemap#how-to-add-a-mime-type-to-a-web-site-or-application)。

## <a name="content-type-mappings"></a>内容类型映射
 通过 HTTP 发布时，.application 文件的内容类型（也称为 MIME 类型）应为“application/x-ms-application”。 如果服务器上安装了 .NET Framework 2.0，则会自动进行设置。 如果未安装，则需要为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序 vroot（或整个服务器）创建 MIME 类型关联。

 如果使用 IIS 服务器进行部署，请运行 <em>inetmgr.</em>exe，为 .application 扩展名添加新的内容类型“application/x-ms-application”。

## <a name="http-compression-issues"></a>HTTP 压缩问题
 通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]，可以执行使用 HTTP 压缩的下载，这是一种 Web 服务器技术，它使用 GZIP 算法压缩数据流，然后再将该数据流发送到客户端。 客户端（本例中为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]）解压缩该流后再读取文件。

 如果使用 IIS，可以轻松启用 HTTP 压缩。 但是，启用 HTTP 压缩时，它仅对某些文件类型（即 HTML 和文本文件）启用。 若要为程序集 (.dll)、XML (.xml)、部署清单 (.application) 和应用程序清单 (.manifest) 启用压缩，必须将这些文件类型添加到 IIS 要压缩的类型列表中   。 在将文件类型添加到部署之前，只会压缩文本和 HTML 文件。

 有关 IIS 的详细说明，请参阅[如何为 HTTP 压缩指定其他文档类型](/troubleshoot/iis/content-types-http-compression)。

## <a name="see-also"></a>另请参阅
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
