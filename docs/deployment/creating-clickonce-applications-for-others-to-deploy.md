---
title: 创建ClickOnce应用程序供其他人部署|Microsoft Docs
description: 了解客户托管ClickOnce 3.5 .NET Framework 3.5 及早期版本的 .NET Framework。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- preserved branding information
- useManifestForTrust element
- customer deployments [ClickOnce]
- multiple ClickOnce deployment and branding
- ClickOnce applications, previous .NET Framework versions
- application manifests [ClickOnce]
- <useManifestForTrust> element
- manifests [ClickOnce]
- trust applications, ClickOnce
- ClickOnce applications, deployed by others
- ClickOnce applications, previous .NET Framework
ms.assetid: d20766c7-4ef3-45ab-8aa0-3f15b61eccaa
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 4d917ff087005264510b512f0a028c5621e74f8a6f79ab80ac9b119d647a1cc8
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403992"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>创建供其他人部署的 ClickOnce 应用程序
并非所有创建应用程序部署ClickOnce都计划自行部署应用程序。 他们中的许多只是使用 ClickOnce 打包应用程序，然后将文件上手给客户，例如大型公司。 客户成为负责在其网络上托管应用程序的人。 本主题讨论在版本 3.5 之前版本 .NET Framework部署中固有的一些问题。 然后，它描述了使用 3.5 版中新的"使用清单建立信任"功能.NET Framework解决方案。 最后，最后提供为仍在使用旧版 ClickOnce 部署的客户创建部署的建议.NET Framework。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>为客户创建部署所涉及的问题
 当你计划向客户提供部署时，会出现若干问题。 第一个问题涉及代码签名。 若要跨网络部署，必须同时使用数字证书ClickOnce部署的部署清单和应用程序清单。 这引发了在签署清单时是使用开发人员证书还是使用客户的证书的问题。

 使用哪个证书至关重要，因为ClickOnce标识基于部署清单的数字签名。 如果开发人员对部署清单进行签署，则如果客户是大型公司，并且公司的多个部门部署了自定义版本的应用程序，则可能会导致冲突。

 例如，假设 Adventure Works 有一个财务部和一个人力资源部门。 这两个部门ClickOnce一个Microsoft Corporation应用程序，该应用程序基于存储在 SQL 数据库中的数据生成报表。 Microsoft 向每个部门提供针对其数据自定义的应用程序版本。 如果应用程序使用相同的 Authenticode 证书进行签名，则尝试使用这两个应用程序的用户会遇到错误，ClickOnce将第二个应用程序视为与第一个应用程序相同。 在这种情况下，客户可能会遇到不可预知且不需要的副作用，包括应用程序在本地存储的任何数据丢失。

 与代码签名相关的另一个问题是部署清单中的 元素，它 `deploymentProvider` ClickOnce在何处查找应用程序更新。 此元素在签名之前必须添加到部署清单中。 如果之后添加此元素，则必须重新签名部署清单。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>要求客户对部署清单进行签名
 这种非唯一部署问题的一种解决方案是让开发人员对应用程序清单进行签名，客户对部署清单进行签名。 虽然此方法有效，但它会引入其他问题。 由于 Authenticode 证书必须仍为受保护的资产，因此客户无法仅将证书授予开发人员对部署进行签名。 尽管客户可以使用随 .NET Framework SDK 免费提供的工具自行对部署清单进行签名，但这可能比客户愿意或能够提供的技术知识要多。 在这种情况下，开发人员通常会创建应用程序、网站或其他机制，客户可以通过这些机制提交其应用程序版本进行签名。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>客户签名对应用程序ClickOnce的影响
 即使开发人员和客户同意客户对应用程序清单进行签名，这也引发了围绕应用程序标识的其他问题，尤其是在它适用于受信任的应用程序部署时。  (有关此功能的信息，请参阅受信任的应用程序部署概述 [。) ](../deployment/trusted-application-deployment-overview.md)假设 Adventure Works 想要配置其客户端计算机，以便 Microsoft Corporation 提供给它们的任何应用程序以完全信任方式运行。 如果 Adventure Works 对部署清单进行签名，ClickOnce将使用 Adventure Work 的安全签名来确定应用程序的信任级别。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>使用用于信任的应用程序清单创建客户部署
 ClickOnce 3.5 .NET Framework包含一项新功能，该功能为开发人员和客户提供了一个新的解决方案，用于实现清单的签名方式。 应用程序ClickOnce支持名为 的新元素，该元素使开发人员能够表示应用程序清单的数字签名是做出信任决策 `<useManifestForTrust>` 时应该使用的内容。 开发人员使用 *ClickOnce* 打包工具（如 *Mage.exe、MageUI.exe* 和 Visual Studio）将此元素包括在应用程序清单中，并将其 Publisher 名称和应用程序名称嵌入到清单中。

 使用 `<useManifestForTrust>` 时，部署清单无需使用证书颁发机构颁发的 Authenticode 证书进行签名。 相反，可以使用所谓的自签名证书对证书进行签名。 自签名证书由客户或开发人员使用标准 .NET Framework SDK 工具生成，然后使用标准部署工具ClickOnce清单。 有关详细信息，请参阅 [MakeCert](/windows/desktop/SecCrypto/makecert)。

 将自签名证书用于部署清单具有几个优点。 通过消除客户获取或创建自己的 Authenticode 证书的要求，简化了客户的部署，同时允许开发人员在应用程序上维护自己的品牌 `<useManifestForTrust>` 标识。 结果是一组更安全且具有唯一应用程序标识的已签名部署。 这消除了将同一应用程序部署到多个客户时可能会发生的潜在冲突。

 有关如何创建已启用 的 ClickOnce 部署的分步信息，请参阅演练：手动部署不需要重新签名并保留品牌信息的 `<useManifestForTrust>` [ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)。

### <a name="how-application-manifest-for-trust-works-at-run-time"></a>用于信任的应用程序清单如何运行时工作
 若要更好地了解使用应用程序清单进行信任的工作原理，请考虑以下示例。 面向 ClickOnce 3.5 .NET Framework应用程序由 Microsoft 创建。 应用程序清单使用 `<useManifestForTrust>` 元素，由 Microsoft 签名。 Adventure Works 使用自签名证书对部署清单进行签名。 Adventure Works 客户端配置为信任由 Microsoft 签名的任何应用程序。

 当用户单击指向部署清单的链接时，ClickOnce在用户计算机上安装应用程序。 证书和部署信息将唯一标识应用程序ClickOnce客户端计算机上。 如果用户尝试从其他位置再次安装同一应用程序，ClickOnce使用此标识来确定客户端上已存在该应用程序。

 接下来ClickOnce验证码证书，该证书用于对应用程序清单进行签名，该证书确定应用程序ClickOnce级别。 由于 Adventure Works 已配置其客户端以信任 Microsoft 签名的任何应用程序，因此ClickOnce应用程序被授予完全信任。 有关详细信息，请参阅 [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

## <a name="create-customer-deployments-for-earlier-versions"></a>为早期版本创建客户部署
 如果开发人员正在将ClickOnce应用程序部署到使用旧版应用程序的客户，.NET Framework？ 以下部分汇总了几个建议的解决方案，以及每个解决方案的优点和缺点。

### <a name="sign-deployments-on-behalf-of-customer"></a>代表客户对部署进行签名
 一种可能的部署策略是让开发人员创建一种机制，以客户自己的私钥代表客户对部署进行签名。 这可以防止开发人员管理私钥或多个部署包。 开发人员只向每个客户提供相同的部署。 客户负责使用签名服务根据自己的环境对其进行自定义。

 此方法的一个缺点是实现该方法所需的时间和费用。 虽然可以使用 .NET Framework SDK 中提供的工具生成此类服务，但它会为产品生命周期添加更多的开发时间。

 如本主题前面所述，另一个缺点是，每个客户的应用程序版本将具有相同的应用程序标识，这可能会导致冲突。 如果这是一个问题，开发人员可以更改生成部署清单时所使用的"名称"字段，为每个应用程序提供唯一的名称。 这将为每个应用程序版本创建单独的标识，并消除任何潜在的标识冲突。 此字段对应于 Mage.exe 的参数，以及 MageUI.exe 中"名称 `-Name` "字段。 

 例如，假设开发人员已创建名为 Application1 的应用程序。 开发人员可以创建多个特定于客户的名称变体的部署，例如 Application1-CustomerA、Application1-CustomerB 等，而不是创建"名称"字段设置为 Application1 的单个部署。

### <a name="deploy-using-a-setup-package"></a>使用安装包进行部署
 第二种可能的部署策略是生成 Microsoft 安装程序项目，以执行应用程序ClickOnce部署。 这可以使用多种不同格式之一提供：作为 MSI 部署、作为安装程序可执行文件 (.EXE) 或作为 cabinet (.cab) 文件以及批处理脚本。

 使用此技术，开发人员将为客户提供一个部署，其中包括应用程序文件、应用程序清单和用作模板的部署清单。 客户将运行安装程序，该程序会提示用户提供部署 URL (服务器或文件共享位置，用户将从该位置安装 ClickOnce 应用程序) 以及数字证书。 安装程序应用程序还可以选择提示输入其他ClickOnce选项，例如更新检查间隔。 收集此信息后，安装程序将生成实际部署清单，对清单进行签名，ClickOnce应用程序发布到指定的服务器位置。

 在这种情况下，客户可以通过三种方式对部署清单进行签名：

1. 客户可以使用证书颁发机构颁发的有效证书 (CA) 。

2. 作为此方法的一种变体，客户可以选择使用自签名证书对部署清单进行签名。 这样做的缺点是，当系统询问用户是否安装它时，它会导致应用程序显示"未知Publisher"字样。 但是，好处是它可以防止较小的客户花费证书颁发机构颁发的证书所需的时间和资金。

3. 最后，开发人员可以在安装包中包括自己的自签名证书。 这引入了本主题前面部分讨论的应用程序标识的潜在问题。

   设置部署项目方法的缺点是生成自定义部署应用程序所需的时间和费用。

### <a name="have-customer-generate-deployment-manifest"></a>使客户生成部署清单
 第三种可能的部署策略是仅将应用程序文件和应用程序清单上线。 在此方案中，客户负责使用 .NET Framework SDK 生成部署清单并签名。

 此方法的缺点是，它要求客户安装 .NET Framework SDK 工具，并拥有具备使用这些工具的开发人员或系统管理员。 某些客户可能要求一个解决方案，而该解决方案几乎不需要或不需要任何技术工作。

## <a name="see-also"></a>请参阅
- [在不ClickOnce的情况下为测试和生产服务器部署应用程序](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [演练：手动部署ClickOnce应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [演练：手动部署不需要重新签名并且保留署名信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)