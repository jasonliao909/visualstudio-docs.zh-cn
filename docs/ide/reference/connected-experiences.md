---
title: Visual Studio 中的连接体验
description: 连接体验从客户端计算机连接到 Internet，并向客户提供服务。
ms.date: 05/20/2021
ms.topic: conceptual
helpviewer_keywords: ''
author: anandmeg
ms.author: meghaanand
manager: jmartens
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.openlocfilehash: 0a54ddd3bdc547d3a6c2fce66696851f634bc6a5
ms.sourcegitcommit: d38d1b083322019663fec7d1d85a4cda456aadca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2021
ms.locfileid: "135534328"
---
# <a name="connected-experiences-in-visual-studio"></a>**Visual Studio 中的连接体验** #

Visual Studio 由客户端软件应用程序和连接体验组成，旨在使你能够更有效地编写代码。 更新 [NuGet](/nuget/consume-packages/install-use-packages-visual-studio) 包、选择 [IntelliCode](/visualstudio/intellicode/overview) 建议以及通过 [Live Share](/visualstudio/liveshare/quickstart/share) 与其他开发人员协作都是连接体验的示例。 

## <a name="choose-whether-these-connected-experiences-are-available-to-use"></a>选择是否可以使用这些连接体验 ##

可以选择要使用的连接体验。 使用某些连接体验需要同意 Visual Studio EULA 的各种附加条款。 这些体验可能是 Microsoft 拥有的联机服务和/或第三方拥有的服务。 例如，当你使用 GitHub 连接体验时，[GitHub 隐私声明](https://docs.github.com/github/site-policy/github-privacy-statement)、[GitHub 服务条款](https://docs.github.com/github/site-policy/github-terms-of-service)、[GitHub 公司服务条款](https://docs.github.com/github/site-policy/github-corporate-terms-of-service)和/或[附加产品条款](https://docs.github.com/github/site-policy/github-additional-product-terms)将适用。 如果你[报告某个问题](../how-to-report-a-problem-with-visual-studio.md)，即表示你同意 [Microsoft 使用条款](https://www.microsoft.com/legal/terms-of-use)和 [Microsoft 隐私声明](https://privacy.microsoft.com/en-us/privacystatement)。 如果使用 NuGet 服务，即表示你同意 [NuGet 使用条款](https://www.nuget.org/policies/Terms)和 [Microsoft 隐私声明](https://privacy.microsoft.com/en-us/privacystatement)。 

安装 Visual Studio 时，[可以选择要安装的工作负载和组件（可选）](../../install/install-visual-studio.md)。 工作负载和组件可以利用第三方软件，并且它们可能会启用连接体验，具体取决于它们的功能。 例如，[下载 Azure 开发工作负载可让你将云应用发布到 Azure](https://visualstudio.microsoft.com/vs/features/azure/)。 根据安装选择，还可使用“工具和选项”菜单来连接、配置和使用连接体验。 例如，可以连接到服务器、添加 Azure 服务身份验证或更改 IntelliCode 或 LiveShare 设置。  

也可使用组织的[防火墙设置](../../install/install-and-use-visual-studio-behind-a-firewall-or-proxy-server.md)来启用或禁用与服务的连接。 请注意，禁用与终结点的连接可能会对相关 Visual Studio 功能的性能产生负面影响或禁用其功能。 

最后，Visual Studio Marketplace 提供了可启用第一方或第三方连接体验的扩展。 Visual Studio Marketplace 受 [Visual Studio Marketplace 使用条款](https://cdn.vsassets.io/v/M146_20190123.39/_content/Microsoft-Visual-Studio-Marketplace-Terms-of-Use.pdf)和 [Microsoft 隐私声明](https://privacy.microsoft.com/en-us/privacystatement)的约束。 每个扩展都需要同意与该产品/服务相关的特定使用条款和隐私声明。  


## <a name="required-service-data"></a>所需的服务数据 ##

所需的服务数据可以包括与连接体验的操作相关的信息，以保持基础服务安全、最新和按照预期执行。 如果选择使用可分析内容的连接体验（例如 IntelliCode），则还会发送和处理为模型选择的代码，以提供连接体验。 所需的服务数据还可包括连接体验执行其任务（例如更新 NuGet 包）所需的信息。 可以通过选择是否使用特定服务来管理所需的服务数据。 如果不使用服务，则不会收集所需的服务数据。 

所需的服务数据与诊断数据不同，因为诊断数据与设备上运行的软件有关。 选择是否参与 [Visual Studio 客户体验改善计划 (VSCEIP) 会控制诊断数据的隐私设置](../visual-studio-experience-improvement-program.md)，但此设置不影响是否发送所需的服务数据。 

## <a name="diagnostic-data-collection"></a>诊断数据收集 ##

诊断数据用于保持 Visual Studio 的安全并使其保持最新，检测、诊断和修复问题，以及进行产品改进。 收集有关在用户设备上运行的 Visual Studio 客户端软件的诊断数据并将其发送给 Microsoft。

选择退出时，将选择退出可选诊断数据收集。 需要完成一些诊断数据收集，才能确保 Visual Studio 是安全的、最新的且正常运行。 所需的诊断数据收集不会因选择退出 [VSCEIP](../visual-studio-experience-improvement-program.md) 而受到影响。 
