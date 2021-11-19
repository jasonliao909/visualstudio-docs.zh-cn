---
title: 创建供其他人部署的 ClickOnce 应用程序 | Microsoft Docs
description: 了解在 .NET Framework 3.5 和 .NET Framework 早期版本中开发的客户托管 ClickOnce 应用程序。
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
ms.openlocfilehash: 032753f2274f17ab99a80b1df45fc5e1627b36de
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665165"
---
# <a name="create-clickonce-applications-for-others-to-deploy"></a>创建供其他人部署的 ClickOnce 应用程序
并非所有要创建 ClickOnce 部署的开发人员都计划自行部署应用程序。 其中很多人只是使用 ClickOnce 来打包应用程序，然后将文件递交给客户（例如大型公司）。 客户成为负责在其网络上托管应用程序的人。 本主题讨论版本 3.5 之前的 .NET Framework 版本中此类部署所固有的一些问题。 然后，它描述了通过使用 .NET Framework 3.5 中新的“使用信任清单”功能提供的新解决方案。 最后，它在结论中给出了为仍在使用早期版本的 .NET Framework 的客户创建 ClickOnce 部署的建议策略。

## <a name="issues-involved-in-creating-deployments-for-customers"></a>为客户创建部署所涉及的问题
 当你计划向客户提供部署时，会出现几个问题。 第一个问题涉及到代码签名。 若要在网络中部署，必须使用数字证书对 ClickOnce 部署的部署清单和应用程序清单进行签名。 这就引出了在对清单进行签名时，是使用开发人员证书还是客户证书的问题。

 使用哪个证书的问题很关键，因为 ClickOnce 应用程序的标识基于部署清单的数字签名。 如果客户是一家大型公司，并且公司的多个部门部署了自定义版本的应用程序，则开发人员签署部署清单可能会导致冲突。

 例如，假设 Adventure Works 有一个财务部门和一个人力资源部门。 这两个部门都授权了来自 Microsoft Corporation 的 ClickOnce 应用程序，该应用程序从 SQL 数据库中存储的数据生成报表。 Microsoft 将为每个部门提供针对其数据自定义的应用程序版本。 如果使用相同的验证码证书对应用程序进行了签名，则尝试使用这两个应用程序的用户会遇到错误，因为 ClickOnce 会将第二个应用程序与第一个应用程序视为完全相同。 在这种情况下，客户可能会遇到不可预知且不想要的副作用，包括丢失应用程序存储在本地的任何数据。

 与代码签名相关的另一个问题是部署清单中的 `deploymentProvider` 元素，该元素告诉 ClickOnce 在何处查找应用程序更新。 必须先将此元素添加到部署清单，然后才能对其进行签名。 如果以后添加此元素，则必须对部署清单进行重新签名。

### <a name="require-the-customer-to-sign-the-deployment-manifest"></a>要求客户对部署清单进行签名
 针对这个非唯一部署问题的一个解决方案是让开发人员签署应用程序清单，而客户签署部署清单。 尽管此方法有效，但它会引入其他问题。 由于验证码证书必须保持为受保护的资产，因此客户不能直接向开发人员授予证书来对部署进行签名。 尽管客户可使用 .NET Framework SDK 中免费提供的工具自行对部署清单进行签名，但这可能需要比客户愿意或能够提供的更多的技术知识。 在这种情况下，开发人员通常会创建一个应用程序、网站或其他机制，通过这些机制，客户可以提交其应用程序版本以进行签名。

### <a name="the-impact-of-customer-signing-on-clickonce-application-security"></a>客户签名对 ClickOnce 应用程序安全性的影响
 即使开发人员和客户同意客户应该对应用程序清单进行签名，这也会引发围绕应用程序标识的其他的问题，特别是当它适用于受信任的应用程序部署时。 （有关此功能的详细信息，请参阅[受信任的应用程序部署概览](../deployment/trusted-application-deployment-overview.md)。）假如 Adventure Works 想要配置自己的客户端计算机，使 Microsoft Corporation 提供的任何应用程序都以完全信任的方式运行。 如果 Adventure Works 对部署清单进行了签名，则 ClickOnce 将使用 Adventure Works 的安全签名来决定该应用程序的信任级别。

## <a name="create-customer-deployments-by-using-application-manifest-for-trust"></a>使用信任应用程序清单创建用户部署
 .NET Framework 3.5 中的 ClickOnce 包含一个新功能，该功能针对如何对清单进行签名的场景，为开发人员和用户提供了一个新的解决方案。 ClickOnce 应用程序清单支持名为 `<useManifestForTrust>` 的新元素，使开发人员能够指示应用程序清单的数字签名应该用于做出信任决策。 开发人员使用 ClickOnce 打包工具（如 Mage.exe、MageUI.exe 和 Visual Studio）将此元素包含在应用程序清单中，并将其发布者姓名和应用程序名称嵌入到清单中 。

 使用 `<useManifestForTrust>` 时，可以不必使用证书颁发机构颁发的验证码证书对部署清单进行签名。 而可以使用所谓的自签名证书对其进行签名。 自签名证书是由客户或开发人员通过使用标准 .NET Framework SDK 工具生成的，然后使用标准 ClickOnce 部署工具应用于部署清单。 有关详细信息，请参阅 [MakeCert](/windows/desktop/SecCrypto/makecert)。

 对部署清单使用自签名证书有几个优点。 使用 `<useManifestForTrust>`，客户不再需要获取或创建自己的验证码证书，为客户简化了部署，同时允许开发人员保留应用程序上自己的品牌标识。 结果是一组更安全且有唯一应用程序标识的已签名部署。 这消除了在向多个客户部署相同应用程序时可能发生的潜在冲突。

 有关如何创建启用了 `<useManifestForTrust>` 的 ClickOnce 部署的分步信息，请参阅[演练：手动部署不需要重新签名并且保留品牌信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)。

### <a name="how-application-manifest-for-trust-works-at-run-time"></a>信任应用程序清单在运行时的工作原理
 若要更好地理解使用信任应用程序清单在运行时的运作方式，请考虑以下示例。 面向 .NET Framework 3.5 的 ClickOnce 应用程序由 Microsoft 创建。 此应用程序清单使用 `<useManifestForTrust>` 元素并由 Microsoft 签名。 Adventure Works 通过使用自签名证书对部署清单进行签名。 Adventure Works 客户端配置为信任 Microsoft 签名的任何应用程序。

 当用户单击部署清单的链接时，ClickOnce 会在用户的计算机上安装该应用程序。 证书和部署信息在客户端计算机上为 ClickOnce 唯一地标识应用程序。 如果用户尝试从不同的位置上再次安装相同的应用程序，ClickOnce 可以使用此标识来确定该应用程序已存在于客户端上。

 接下来，ClickOnce 检查用于对应用程序清单签名的验证码证书，该证书决定了 ClickOnce 将授予的信任级别。 由于 Adventure Works 已将其客户端配置为信任 Microsoft 签名的任何应用程序，因此该 ClickOnce 应用程序被授予完全信任。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

## <a name="create-customer-deployments-for-earlier-versions"></a>为早期版本创建客户部署
 如果开发人员要将 ClickOnce 应用程序部署给使用旧版 .NET Framework 的客户，该怎么办？ 以下部分总结了几个建议的解决方案，以及各解决方案的优点和缺点。

### <a name="sign-deployments-on-behalf-of-customer"></a>代表客户对部署进行签名
 一个可能的部署策略是让开发人员创建一个通过使用客户的私钥，代表客户对部署进行签名的机制。 这使得开发人员不必管理私钥或多个部署包。 开发人员只向每个客户提供相同的部署。 由客户自行决定是否使用签名服务针对环境对其进行自定义。

 此方法的一个缺点是实现该方法所需的时间和费用。 虽然此服务可以通过使用 .NET Framework SDK 提供的工具来生成，但它将向产品生命周期增加更多的开发时间。

 正如本主题前面所述，另一个缺点是每个客户的应用程序版本将会有相同的应用程序标识，这可能导致冲突。 如果这是一个令人担忧的问题，开发人员可以更改生成部署清单时所用的“名称”字段，为每个应用程序提供一个唯一名称。 这将为每个应用程序版本创建一个单独的标识，并消除任何潜在的标识冲突。 此字段对应于 Mage.exe 的 `-Name` 参数，以及 MageUI.exe 中“名称”选项卡上的“名称”字段 。

 例如，假设开发人员创建了一个名为 Application1 的应用程序。 开发人员不需要创建一个“名称”字段设置为“Application1”的部署，而可以使用该名称的客户特定变体创建多个部署，如 Application1-CustomerA 和 Application1-CustomerB 等。

### <a name="deploy-using-a-setup-package"></a>使用安装包进行部署
 另一个可能的部署策略是生成一个 Microsoft 安装项目，执行 ClickOnce 应用程序的最初部署。 这可以使用几种不同的格式之一提供：作为 MSI 部署、作为安装可执行文件 (.EXE) 或作为带有批处理脚本的 cabinet (.cab) 文件。

 使用此方法，开发人员将向客户提供一个包括应用程序文件、应用程序清单和作为模板的部署清单的部署。 客户将运行安装程序，该程序将会提示客户提供部署 URL（用户安装 ClickOnce 应用程序的服务器或文件共享位置）和数字证书。 该安装应用程序还可以选择提示客户提供其他 ClickOnce 配置选项，例如更新检查间隔。 收集此信息后，安装程序会生成真实的部署清单，对其进行签名，然后将 ClickOnce 应用程序发布到指定的服务器位置。

 在这种情况下，客户可以通过三种方式对部署清单进行签名：

1. 客户可以使用证书颁发机构 (CA) 颁发的有效证书。

2. 作为此方法的一种变化形式，客户可以选择使用自签名证书对其部署清单进行签名。 这种方法的缺点是，当询问用户是否安装时，它会导致应用程序显示“未知发布者”字样。 但优点在于，它可以防止小型客户花费所需时间和金钱以获得由证书颁发机构颁发的证书。

3. 最后，开发人员可以在安装包中包含自己的自签名证书。 这会引入本主题前面所述的应用程序标识的潜在问题。

   安装部署项目方法的缺点是构建自定义部署应用程序所需的时间和费用。

### <a name="have-customer-generate-deployment-manifest"></a>让客户生成部署清单
 第三个可能的部署策略是仅将应用程序文件和应用程序清单交给客户。 在此场景中，客户负责使用 .NET Framework SDK 生成并签署部署清单。

 此方法的缺点是要求客户安装 .NET Framework SDK 工具，并有可熟练使用这些工具的开发人员或系统管理员。 有些客户可能需要一个他们只需要进行很少的技术工作或不需要进行技术工作的解决方案。

## <a name="see-also"></a>另请参阅
- [在不重新签名的情况下为测试和生产服务器部署 ClickOnce 应用程序](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
- [演练：手动部署不需要重新签名并且保留署名信息的 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-app-no-re-signing-required.md)