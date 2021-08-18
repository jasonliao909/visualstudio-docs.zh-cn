---
title: '排查 (ClickOnce部署错误) '
description: 本文介绍在部署应用程序时可能会发生的常见ClickOnce并提供解决每个问题的步骤。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: troubleshooting
f1_keywords:
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.UncRequired
- Microsoft.VisualStudio.Publish.ClickOnceProvider.ErrorPrompt.NoInstallUrl
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- deploying applications, ClickOnce
- troubleshooting ClickOnce deployments
- ClickOnce deployment, troubleshooting
ms.assetid: 22dfe8f1-8271-4708-9c25-6bbb13920ac8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4cfbfa1c13a6006303b1fd0fa164d78c7f4e6b9f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089818"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>ClickOnce 部署中特定错误的疑难解答
本文列出了部署应用程序时可能会发生的以下常见错误，并提供 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 解决每个问题的步骤。

## <a name="general-errors"></a>常规错误

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>尝试查找应用程序文件时，不会执行任何操作，或者 XML Internet Explorer，或者你会收到"运行"或"另存为"对话框
 此错误可能是由于内容类型 (也称为 MIME 类型) 服务器或客户端上未正确注册。

 首先，请确保将服务器配置为将 *.application* 扩展与内容类型"application/x-ms-application"关联。

 如果服务器配置正确，请检查计算机上是否.NET Framework 2.0。 如果已安装 .NET Framework 2.0，但仍出现此问题，请尝试卸载并重新安装 .NET Framework 2.0，以在客户端上重新注册内容类型。

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>错误消息显示"无法检索应用程序。 部署中缺少的文件"或"应用程序下载已中断，请检查网络错误，稍后重试"
 此消息指示无法下载清单引用的一 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 个或多个文件。 调试此错误的最简单方法是尝试下载表示无法下载 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的 URL。 下面是一些可能的原因：

- 如果日志文件显示" (403) 禁止访问"或" (404) 未找到"，请验证 Web 服务器已配置，以便它不会阻止下载此文件。 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。

- 如果 *.config* 文件被服务器阻止，请参阅本文稍后的"尝试安装具有 .config 文件的应用程序时下载 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 错误"部分。

- 确定是否由于部署清单中的 URL 指向与用于激活的 `deploymentProvider` URL 不同的位置而发生此错误。

- 确保服务器上存在所有文件; [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 日志应会告知找不到哪个文件。

- 查看是否有网络连接问题;如果客户端计算机在下载过程中脱机，则会收到此消息。

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>尝试安装包含文件ClickOnce的应用程序时出现.config错误
 默认情况下，基于Visual Basic Windows的应用程序包含一App.config文件。 当用户尝试从使用 Windows Server 2003 的 Web 服务器进行安装时，将出现问题，因为该操作系统 *出于* 安全原因.config文件安装。 若要 *启用.config文件*，请单击"发布选项"对话框中的"使用 **.deploy"****文件** 扩展名。

 还必须设置内容类型 (也称为 MIME 类型) 适用于 .application、.manifest 和 .deploy 文件。 有关详细信息，请参阅 Web 服务器文档。

 有关详细信息，请参阅 服务器中的"Windows Server 2003：锁定的内容类型["和部署中的客户端ClickOnce问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>错误消息："应用程序格式不正确;"日志文件包含"XML 签名无效"
 确保更新了清单文件，并再次对该文件进行了签名。 使用 或 重新发布应用程序 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] ，Mage重新对应用程序进行签名。

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>你在服务器上更新了应用程序，但客户端不会下载更新
 可以通过完成以下任务之一来解决此问题：

- 检查 `deploymentProvider` 部署清单中的 URL。 确保更新指向的同一位置中的 `deploymentProvider` 位。

- 验证部署清单中的更新间隔。 如果此间隔设置为定期间隔（例如每六小时一次）将不会扫描更新，直到此 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 间隔已过。 可以更改清单，以每次启动应用程序时扫描更新。 在开发期间，更改更新间隔是验证是否安装了更新的便捷选项，但会减慢应用程序激活速度。

- 尝试在应用程序上再次"开始"菜单。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可能在后台检测到更新，但会提示你在下次激活时安装位。

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>在更新期间，你收到具有以下日志条目的错误："部署中的引用与应用程序清单中定义的标识不匹配"
 发生此错误的原因可能是你手动编辑了部署和应用程序清单，并且导致一个清单中程序集的标识说明与另一个清单不同步。 程序集的标识包括其名称、版本、区域性和公钥标记。 检查清单中的标识说明，并更正任何差异。

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>首次从本地磁盘或 CD-ROM 激活成功，但"开始"菜单中的后续激活不会成功
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用部署提供程序 URL 接收应用程序的更新。 验证 URL 指向的位置是否正确。

#### <a name="error-cannot-start-the-application"></a>错误："无法启动应用程序"
 此错误消息通常指示将此应用程序安装到存储时 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 出现问题。 应用程序出错或存储已损坏。 日志文件可能会告知错误发生的位置。

 应执行以下操作：

- 验证部署清单的标识、应用程序清单的标识以及主应用程序 EXE 的标识是否都是唯一的。

- 验证文件路径是否不超过 100 个字符。 如果应用程序包含过长的文件路径，则可能会超出可存储的最大路径的限制。 请尝试缩短路径并重新安装。

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>应用程序配置文件中的 PrivatePath 设置不受到遵守
 若要使用 PrivatePath (Fusion 探测) ，应用程序必须请求完全信任权限。 尝试更改应用程序清单以请求完全信任，然后重试。

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>卸载期间出现一条消息，指出"未能卸载应用程序"
 此消息通常指示应用程序已被删除或存储已损坏。 单击" **确定"** 后， **将删除** "添加/删除程序"条目。

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>在安装过程中，将显示一条消息，指出未安装平台依赖项
 在 GAC 数据库全局程序集缓存 (缺少) 运行应用程序所需的先决条件。

## <a name="publishing-with-visual-studio"></a>使用 Visual Studio

#### <a name="publishing-in-visual-studio-fails"></a>在 Visual Studio 中发布失败
 确保有权发布到目标服务器。 例如，如果你以普通用户而不是管理员身份登录到终端服务器计算机，则你可能没有发布到本地 Web 服务器所需的权限。

 如果要使用 URL 发布，请确保目标计算机已启用FrontPage 服务器扩展。

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>错误消息：无法创建网站 \<site> ""。 未安装用于与FrontPage 服务器扩展通信的组件。
 确保在要发布Microsoft Visual Studio计算机上安装了 Web 创作组件。 对于 Express 用户，默认情况下不安装此组件。 有关详细信息，请参阅 [http://go.microsoft.com/fwlink/?LinkId=102310](https://support.microsoft.com/help/945358)。

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>错误消息：找不到文件"Microsoft.Windows。Common-Controls, Version=6.0.0.0, Culture=*, PublicKeyToken=6595b64144ccf1df, ProcessorArchitecture= \* , Type=win32'
 尝试发布启用了视觉样式的 WPF 应用程序时，会出现此错误消息。 若要解决此问题，请参阅 [如何：发布启用了视觉样式的 WPF 应用程序](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)。

## <a name="using-mage"></a>使用 Mage

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>你尝试使用证书存储中的证书和收到的空白消息框进行签名
 在 **"签名** "对话框中，必须：

- 选择 **"使用存储的证书签名"，** 然后

- 从列表中选择证书;第一个证书不是默认选择。

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>单击"不签名"按钮会导致异常
 此问题是一个已知 bug。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]所有清单都需要签名。 只需选择其中一个签名选项，然后单击"确定 **"。**

## <a name="additional-errors"></a>其他错误
 下表显示了客户端计算机用户在安装应用程序时可能收到的一些常见 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 错误消息。 每个错误消息都列在错误最可能原因的说明旁边。

| 错误消息 | 说明 |
| - | - |
| 无法启动应用程序。 请联系应用程序发布者。<br /><br /> 无法启动应用程序。 请联系应用程序供应商寻求帮助。 | 这些是无法启动应用程序且找不到其他特定原因时发生的一般错误消息。 这通常意味着应用程序以某种方式已损坏，或者 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 存储已损坏。 |
| 无法继续。 应用程序的格式不正确。 请联系应用程序发布者寻求帮助。<br /><br /> 应用程序验证未成功。 无法继续。<br /><br /> 无法检索应用程序文件。 部署中的文件已损坏。 | 部署中的清单文件之一在语法上无效，或者包含无法与相应文件协调的哈希。 此错误可能还指示程序集内嵌入的清单已损坏。 重新创建部署并重新编译应用程序，或手动查找并修复清单中的错误。 |
| 无法检索应用程序。 身份验证错误。<br /><br /> 应用程序安装未成功。 在服务器上找不到应用程序文件。 请联系应用程序发布者或管理员寻求帮助。 | 无法下载部署中的一个或多个文件，因为你无权访问它们。 这可能是由 Web 服务器返回的 403 禁止访问错误导致的，如果部署中的一个文件以使 Web 服务器视为受保护文件的扩展名结束，则可能会发生此错误。 此外，包含一个或多个应用程序文件的目录可能需要用户名和密码才能访问。 |
| 无法下载应用程序。 应用程序缺少所需的文件。 请联系应用程序供应商或系统管理员寻求帮助。 | 在服务器上找不到应用程序清单中列出的一个或多个文件。 检查是否上传了部署的所有依赖文件，然后重试。 |
| 应用程序下载未成功。 请检查网络连接，或联系系统管理员或网络服务提供商。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 无法与服务器建立网络连接。 检查服务器的可用性和网络状态。 |
| URLDownloadToCacheFile 失败，HRESULT ' \<number> '。 尝试下载''时 \<file> 出错。 | 如果用户在部署目标计算机上设置了 Internet Explorer 高级安全选项"在安全模式和不安全模式之间更改时发出警告"，并且要安装的 ClickOnce 应用程序的安装 URL 从不安全站点重定向到安全站点 (，反之亦然) ，则安装将失败，因为 Internet Explorer 警告会中断安装。<br /><br /> 若要解决此错误，可以执行以下任务之一：<br /><br /> - 清除安全选项。<br />- 确保不会以更改安全模式的方式重定向安装 URL。<br />- 完全删除重定向，并指向实际的安装 URL。 |
| 写入硬盘时出错。 磁盘上的空间可能不足。 请联系应用程序供应商或系统管理员寻求帮助。 | 这可能表示存储空间不足，无法存储应用程序，但它也可能表示尝试将应用程序文件保存到驱动器时出现更常规的 I/O 错误。 |
| 无法启动应用程序。 磁盘上没有足够的可用空间。 | 硬盘已满。 清除空间，并尝试再次运行应用程序。 |
| 尝试一次加载的已部署激活过多。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 限制可同时启动的不同应用程序的数量。 这在很大程度上是为了帮助防止恶意尝试对本地服务进行拒绝服务攻击;尝试连续重复启动同一应用程序的用户最终只会获得应用程序的单个实例。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] |
| 无法通过网络激活快捷方式。 | 应用程序的快捷方式 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 只能在本地硬盘上启动。 无法通过打开指向远程服务器上快捷方式文件的 URL 来启动它们。 |
| 应用程序太大，在部分信任中联机运行。 请联系应用程序供应商或系统管理员寻求帮助。 | 在部分信任下运行的应用程序不能大于联机应用程序配额大小的一半，该配额默认为 250 MB。 |

## <a name="see-also"></a>请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)