---
title: 错误疑难解答（ClickOnce 部署）
description: 本文介绍部署 ClickOnce 应用程序时可能出现的常见错误，并提供解决每个问题的步骤。
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
ms.openlocfilehash: 1a518074d07f970034eaaf14eb6d427052e22c22
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129431401"
---
# <a name="troubleshoot-specific-errors-in-clickonce-deployments"></a>ClickOnce 部署中特定错误的疑难解答
本文列出了部署 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时可能出现的以下常见错误，并提供解决每个问题的步骤。

## <a name="general-errors"></a>常规错误

#### <a name="when-you-try-to-locate-an-application-file-nothing-occurs-or-xml-renders-in-internet-explorer-or-you-receive-a-run-or-save-as-dialog-box"></a>尝试查找应用程序文件时，不执行任何操作，或者在 Internet Explorer 中呈现 XML，或者出现“运行”或“另存为”对话框
 此错误可能是由于内容类型（也称为 MIME 类型）在服务器或客户端上未正确注册导致的。

 首先，请确保将服务器配置为将 .application 扩展与内容类型“application/x-ms-application”关联。

 如果服务器配置正确，请检查计算机上是否安装了 .NET Framework 2.0。 如果已安装 .NET Framework 2.0，但仍出现此问题，请尝试卸载并重新安装 .NET Framework 2.0，以在客户端上重新注册内容类型。

#### <a name="error-message-says-unable-to-retrieve-application-files-missing-in-deployment-or-application-download-has-been-interrupted-check-for-network-errors-and-try-again-later"></a>错误消息显示“无法检索应用程序。 部署中缺少文件”或“应用程序下载已中断，请检查网络错误，稍后重试”
 此消息指示无法下载 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单引用的一个或多个文件。 调试此错误最简单的方法是尝试下载 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 表示无法下载的 URL。 可能的原因如下：

- 如果日志文件显示“(403) 禁止访问”或“(404) 未找到”，请验证 Web 服务器已配置，以便它不会阻止下载此文件。 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)。

- 如果 .config 文件被服务器阻止，请参阅本文后面的“尝试安装具有 .config 文件的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时下载出错”部分。

- 确定是否由于部署清单中的 `deploymentProvider` URL 指向与用于激活的 URL 不同的位置而发生此错误。

- 确保服务器上存在所有文件；[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 日志应该会告知你未找到的文件。

- 查看是否存在网络连接问题；如果客户端计算机在下载过程中脱机，则你会收到此消息。

#### <a name="download-error-when-you-try-to-install-a-clickonce-application-that-has-a-config-file"></a>尝试安装包含 .config 文件的 ClickOnce 应用程序时下载出错
 默认情况下，基于 Windows 的 Visual Basic 应用程序包含 App.config 文件。 当用户尝试从使用 Windows Server 2003 的 Web 服务器进行安装时，将出现问题，因为该操作系统出于安全原因会阻止安装 .config 文件。 若要使 .config 文件顺利安装，请单击“发布选项”对话框中的“使用‘.deploy’文件扩展名”。

 还必须为 .application、.manifest 和 .deploy 文件设置相应的内容类型（也称为 MIME 类型）。 有关详细信息，请参阅 Web 服务器文档。

 有关详细信息，请参阅 [ClickOnce 部署中的服务器和客户端配置问题](../deployment/server-and-client-configuration-issues-in-clickonce-deployments.md)中的“Windows Server 2003：锁定的内容类型”。

#### <a name="error-message-application-is-improperly-formatted-log-file-contains-xml-signature-is-invalid"></a>错误消息：“应用程序格式不正确”；日志文件包含“XML 签名无效”
 确保更新了清单文件，并再次对该文件进行了签名。 使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 或使用 Mage 重新发布应用程序，以重新对应用程序进行签名。

#### <a name="you-updated-your-application-on-the-server-but-the-client-does-not-download-the-update"></a>你在服务器上更新了应用程序，但客户端不会下载更新
 可以通过完成以下任务之一来解决此问题：

- 检查部署清单的 `deploymentProvider` URL。 确保更新 `deploymentProvider` 指向的同一位置中的位。

- 验证部署清单中的更新间隔。 如果此间隔设置为定期间隔（例如每六小时一次），[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 将不会扫描更新，直到此间隔已过。 可以更改清单，以在每次启动应用程序时扫描更新。 在开发期间，更改更新间隔是验证是否正在安装更新的便捷选项，但会减慢应用程序激活速度。

- 尝试在“开始”菜单上再次启动应用程序。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可能在后台检测到更新，但会在下次激活时提示你安装位。

#### <a name="during-update-you-receive-an-error-that-has-the-following-log-entry-the-reference-in-the-deployment-does-not-match-the-identity-defined-in-the-application-manifest"></a>在更新期间，你收到具有以下日志条目的错误：“部署中的引用与应用程序清单中定义的标识不匹配”
 出现此错误的原因可能是你手动编辑了部署和应用程序清单，并且导致一个清单中程序集的标识说明与另一个清单不同步。 程序集标识包括其名称、版本、区域性和公钥标记。 检查清单中的标识说明，并更正任何差异。

#### <a name="first-time-activation-from-local-disk-or-cd-rom-succeeds-but-subsequent-activation-from-start-menu-does-not-succeed"></a>首次从本地磁盘或 CD-ROM 激活成功，但“开始”菜单中的后续激活未成功
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用部署提供程序 URL 来接收应用程序更新。 验证 URL 指向的位置是否正确。

#### <a name="error-cannot-start-the-application"></a>错误：“无法启动应用程序”
 此错误消息通常指示在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 存储中安装此应用程序时出现问题。 应用程序出错或存储损坏。 日志文件可能会告知错误发生的位置。

 应执行以下操作：

- 验证部署清单的标识、应用程序清单的标识以及主应用程序 EXE 的标识是否都是唯一的。

- 验证文件路径是否不超过 100 个字符。 如果应用程序包含过长的文件路径，则可能会超出可存储的最大路径的限制。 请尝试缩短路径并重新安装。

#### <a name="privatepath-settings-in-application-config-file-are-not-honored"></a>应用程序配置文件中的 PrivatePath 设置不受支持
 若要使用 PrivatePath（融合探测路径），应用程序必须请求完全信任权限。 尝试更改应用程序清单以请求完全信任，然后重试。

#### <a name="during-uninstall-a-message-appears-saying-failed-to-uninstall-application"></a>卸载期间出现一条消息，指示“未能卸载应用程序”
 此消息通常表示应用程序已被删除或存储损坏。 单击“确定”后，将删除“添加/删除程序”项。

#### <a name="during-installation-a-message-appears-that-says-that-the-platform-dependencies-are-not-installed"></a>在安装过程中，将显示一条消息，指示未安装平台依赖项
 你未满足应用程序运行所需的 GAC（全局程序集缓存）的先决条件。

## <a name="publishing-with-visual-studio"></a>通过 Visual Studio 发布

#### <a name="publishing-in-visual-studio-fails"></a>Visual Studio 发布失败
 确保有权发布到目标服务器。 例如，如果你以普通用户而不是管理员身份登录到终端服务器计算机，则你可能没有发布到本地 Web 服务器所需的权限。

 如果要使用 URL 进行发布，请确保目标计算机已启用 FrontPage 服务器扩展。

#### <a name="error-message-unable-to-create-the-web-site-site-the-components-for-communicating-with-frontpage-server-extensions-are-not-installed"></a>错误消息：无法创建网站“\<site>”。 未安装用于与 FrontPage 服务器扩展通信的组件。
 确保在要发布的计算机上安装 Microsoft Visual Studio Web 创作组件。 对于 Express 用户，默认情况下不安装此组件。

#### <a name="error-message-could-not-find-file-microsoftwindowscommon-controls-version6000-culture-publickeytoken6595b64144ccf1df-processorarchitecture-typewin32"></a>错误消息：找不到文件“Microsoft.Windows.Common-Controls, Version=6.0.0.0, Culture=*, PublicKeyToken=6595b64144ccf1df, ProcessorArchitecture=\*, Type=win32”
 尝试发布启用了视觉样式的 WPF 应用程序时，将出现此错误消息。 要解决此问题，请参阅[操作说明：发布启用了视觉样式的 WPF 应用程序](../deployment/how-to-publish-a-wpf-application-with-visual-styles-enabled.md)。

## <a name="using-mage"></a>使用 Mage

#### <a name="you-tried-to-sign-with-a-certificate-in-your-certificate-store-and-a-received-blank-message-box"></a>你尝试使用证书存储中的证书进行签名，但收到空白消息框
 在“签名”对话框中，你必须：

- 选择“使用存储的证书签名”，然后

- 从列表中选择证书；第一个证书不是默认选择。

#### <a name="clicking-the-dont-sign-button-causes-an-exception"></a>单击“不签名”按钮会导致异常
 此问题是一个已知 bug。 所有 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单都需要签名。 选择签名选项之一，然后单击“确定”。

## <a name="additional-errors"></a>其他错误
 下表显示了客户端计算机用户在安装 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时可能收到的一些常见错误消息。 每个错误消息都列在错误最可能的原因的说明旁边。

| 错误消息 | 说明 |
| - | - |
| 无法启动应用程序。 请联系应用程序发布者。<br /><br /> 无法启动应用程序。 请联系应用程序供应商寻求帮助。 | 这些是无法启动应用程序且找不到其他特定原因时出现的一般错误消息。 这通常意味着应用程序以某种方式损坏了，或者 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 存储损坏。 |
| 无法继续。 应用程序格式不正确。 请联系应用程序发布者寻求帮助。<br /><br /> 应用程序验证未成功。 无法继续。<br /><br /> 无法检索应用程序文件。 部署中的文件损坏。 | 部署中的清单文件之一在语法上无效，或者包含无法与相应文件协调的哈希。 此错误可能还指示程序集内嵌入的清单已损坏。 重新创建部署并重新编译应用程序，或手动查找并修复清单中的错误。 |
| 无法检索应用程序。 身份验证错误。<br /><br /> 应用程序安装失败。 在服务器上找不到应用程序文件。 请联系应用程序发布者或管理员寻求帮助。 | 无法下载部署中的一个或多个文件，因为你无权访问它们。 这可能是由 Web 服务器返回的 403 禁止访问错误导致的，如果部署中的一个文件以使 Web 服务器视为受保护文件的扩展名结尾，则可能会发生此错误。 此外，包含一个或多个应用程序文件的目录可能需要用户名和密码才能访问。 |
| 无法下载应用程序。 应用程序缺少所需的文件。 请联系应用程序供应商或系统管理员寻求帮助。 | 在服务器上找不到应用程序清单中列出的一个或多个文件。 检查是否上传了部署的所有从属文件，然后重试。 |
| 应用程序下载失败。 请检查网络连接，或联系系统管理员或网络服务提供商。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 无法与服务器建立网络连接。 检查服务器的可用性和网络状态。 |
| URLDownloadToCacheFile 失败，显示 HRESULT“\<number>”。 尝试下载“\<file>”时出错。 | 如果用户在部署目标计算机上设置了 Internet Explorer 高级安全选项“在安全和非安全模式之间切换时发出警告”，并且要安装的 ClickOnce 应用程序的安装 URL 从非安全站点重定向到安全站点（反之亦然），则安装将失败，因为 Internet Explorer 警告会中断它。<br /><br /> 若要解决此错误，可执行下列任务之一：<br /><br /> -   清除安全选项。<br />-   确保不会以更改安全模式的方式重定向安装 URL。<br />-   完全删除重定向，并指向实际安装 URL。 |
| 写入硬盘时出错。 磁盘上的可用空间可能不足。 请联系应用程序供应商或系统管理员寻求帮助。 | 这可能表示磁盘空间不足，无法存储应用程序，但它也可能表示尝试将应用程序文件保存到驱动器时出现更常规的 I/O 错误。 |
| 无法启动应用程序。 磁盘上的可用空间不足。 | 硬盘已满。 清除空间，并尝试再次运行应用程序。 |
| 尝试一次加载太多已部署的激活。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 限制可同时启动的不同应用程序的数量。 这在很大程度上是为了帮助防止恶意尝试对本地 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 服务发起拒绝服务攻击；尝试连续重复启动同一应用程序的用户最终只会获得应用程序的单个实例。 |
| 无法通过网络激活快捷方式。 | [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的快捷方式只能在本地硬盘上启动。 无法通过打开指向远程服务器上快捷方式文件的 URL 来启动它们。 |
| 应用程序太大，无法在部分信任的情况下联机运行。 请联系应用程序供应商或系统管理员寻求帮助。 | 在部分信任情况下运行的应用程序不能大于联机应用程序配额大小（默认为 250 MB）的一半。 |

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [ClickOnce 部署疑难解答](../deployment/troubleshooting-clickonce-deployments.md)
- [Visual Studio 故障排除](/troubleshoot/visualstudio/welcome-visual-studio/)
