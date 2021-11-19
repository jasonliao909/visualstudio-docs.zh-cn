---
title: ClickOnce验证码|Microsoft Docs
description: 了解验证码用于验证应用程序真实性的证书。 了解如何验证和存储证书。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- .pfx files
- ClickOnce deployment, Authenticode
- Authenticode, ClickOnce
- ClickOnce deployment, certificates
- ClickOnce deployment, security
ms.assetid: ab5b6712-f32a-4e33-842f-e88ab4818ccf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 12915e34da0c2db4dfe2db51167874175963ccb0
ms.sourcegitcommit: 541871db9065c4fb1b21c24f980c563991b183c7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "129431583"
---
# <a name="clickonce-and-authenticode"></a>ClickOnce 和 Authenticode
*验证码* 是使用行业标准加密，通过验证应用程序发行者真实性的数字证书对应用程序代码进行签名的 Microsoft 技术。 通过对应用程序部署使用验证码， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可以降低遭受特洛伊木马程序攻击的风险。 特洛伊木马程序是一种病毒或其他有害的程序，恶意的第三方将其伪装成来自已确认且可信任的源的合法程序。 用数字证书为 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署签名是用于验证程序集和文件是否经过篡改的可选步骤。

 以下各节描述了验证码中使用的不同类型的数字证书，如何使用证书颁发机构 (CA) 验证证书，时间戳在证书中的角色，以及可用于证书的存储方法。

## <a name="authenticode-and-code-signing"></a>验证码和代码签名
 *数字证书* 是一个包含一个加密公钥/私钥对和元数据的文件，元数据描述了向其颁发证书的发行者以及颁发证书的机构。

 有各种类型的验证码证书。 每种验证码证书为不同类型的签名而配置。 对于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，必须具有对代码签名有效的验证码证书。 如果尝试使用其他类型证书（如数字电子邮件证书）对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序进行签名，将不起作用。 有关详细信息，请参阅 [代码签名简介](/windows/desktop/seccrypto/cryptography-tools)。

 可以通过以下三种方法之一获取代码签名证书：

- 从证书供应商处购买证书。

- 从组织中负责创建数字证书的组中接收证书。

- 使用 PowerShell cmdlet New-SelfSignedCertificate或MakeCert.exe *，从而* 生成自己的证书 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 。

### <a name="how-using-certificate-authorities-helps-users"></a>使用证书颁发机构对用户的好处
 使用 New-selfsignedcertificate 生成的证书或 *MakeCert.exe* 通常称为实用工具 *自发证书* 或 *测试证书*。这种证书的工作方式与.NET Framework 中 *.snk* 文件的工作方式大致相同。 它只包含公钥/私钥加密密钥对，不包含有关发行者的可验证信息。 可以使用自发证书在 Intranet 上部署具有高信任级别的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 但是，当这些应用程序在客户端计算机上运行时， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 会将它们标识为来自未知发行者。 默认情况下，使用自发证书签名并在 Internet 上部署的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序不能使用受信任的应用程序部署。

 相反，从 CA（如证书供应商或企业内部部门）收到的证书可以为你的用户提供更高的安全性。 该证书不仅会标识已签名软件的发行者，还会通过与签发该证书的 CA 进行核实来验证发行者的身份。 如果 CA 不是根证书颁发机构，验证码还会沿证书链回溯到根颁发机构来验证该 CA 是否有权颁发证书。 为了提高安全性，应尽量使用 CA 颁发的证书。

 有关生成自证书的信息，请参阅 [New-SelfSignedCertificate](/powershell/module/pki/new-selfsignedcertificate) 或 [MakeCert](/windows/desktop/SecCrypto/makecert)。

### <a name="timestamps"></a>时间戳
 用于对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序签名的证书在特定时间长度（通常为 12 个月）后会过期。 为了避免不断使用新证书对应用程序重新签名， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 支持时间戳。 使用时间戳对应用程序签名，只要时间戳有效，即使过期之后证书仍将被接受。 这将允许下载和运行证书已过期，但时间戳有效的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 还允许使用过期证书的已安装应用程序继续下载和安装更新。

 若要在应用程序服务器中包含时间戳，时间戳服务器必须可用。 有关如何选择时间戳服务器的信息，请参阅 [How to: Sign Application and Deployment Manifests](../ide/how-to-sign-application-and-deployment-manifests.md)。

### <a name="update-expired-certificates"></a>更新过期的证书
 在早期版本的 .NET framework 中，更新证书已过期的应用程序可能导致该应用程序无法正常工作。 若要解决此问题，请使用以下方法之一：

- 在 Windows XP 上将 .NET Framework 更新至 2.0 SP1 版本或更高版本，或在 Windows Vista 上将其更新至 3.5 版或更高版本。

- 卸载该应用程序，并重新安装具有有效证书的新版本。

### <a name="store-certificates"></a>存储证书

- 可以在文件系统上将证书存储为.pfx 文件，或将其存储在密钥容器中。 Windows 域上的用户可拥有若干数目的密钥容器。 默认情况下，MakeCert.exe 会将证书存储在个人密钥容器中，除非指定将其保存为 .pfx。 用于创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 工具 Mage.exe 和 MageUI.exe，借助这些工具可以使用上述任一方式中存储的证书。

## <a name="see-also"></a>另请参阅
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)