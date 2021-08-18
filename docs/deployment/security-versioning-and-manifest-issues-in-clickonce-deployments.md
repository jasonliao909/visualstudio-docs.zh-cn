---
title: '安全/版本控制/清单问题 (ClickOnce) '
description: 了解有关ClickOnce、应用程序版本控制、清单语法和语义的问题，这些问题可能导致ClickOnce部署不成功。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- versioning, ClickOnce applications
- ClickOnce applications, Windows Vista User Account Control
- ClickOnce applications, versioning issues
- security, ClickOnce applications
- Windows 7, ClickOnce deployments
- ClickOnce applications, manifest issues
- User Account Control, ClickOnce applications
- Windows Vista, ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, security issues
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: b6048aeb6972b2f60c8ba421e9a1593ba2cf42a7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035615"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 部署中的安全、版本控制和清单问题

安全性、应用程序版本控制以及清单语法和语义存在各种问题， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可能会导致 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署不成功。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce Windows Vista 用户帐户控制

在 中，应用程序默认以标准用户身份运行，即使当前用户使用具有管理员 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 权限的帐户登录。 如果应用程序必须执行需要管理员权限的操作，它会告知操作系统，然后提示用户输入其管理员凭据。 此功能名为 User Account Control (UAC) ，可防止应用程序在未经用户显式批准的情况下做出可能影响整个操作系统的更改。 Windows应用程序通过指定其应用程序清单的 部分中的 属性来 `requestedExecutionLevel` `trustInfo` 声明它们需要此权限提升。

由于存在向应用程序公开安全提升攻击的风险，因此，如果为客户端启用了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] UAC，则应用程序无法请求权限提升。 任何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 尝试将其属性设置为 或 `requestedExecutionLevel` `requireAdministrator` `highestAvailable` 的应用程序将不会安装在 上 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 。

在某些情况下，由于 上的安装程序检测逻辑，应用程序可能会尝试使用管理员 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 权限运行 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 。 在这种情况下，可以将应用程序清单中的 属性 `requestedExecutionLevel` 设置为 `asInvoker` 。 这会使应用程序本身在没有提升的情况下运行。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 会自动将此属性添加到所有应用程序清单。

如果开发的应用程序在应用程序的整个生存期内需要管理员权限，则应考虑改为使用 Windows Installer (MSI) 技术部署该应用程序。 有关详细信息，请参阅 Windows[安装程序基础知识](../extensibility/internals/windows-installer-basics.md)。

## <a name="online-application-quotas-and-partial-trust-applications"></a>联机应用程序配额和部分信任应用程序

如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序联机运行而不是通过安装运行，则它必须位于为联机应用程序保留的配额范围内。 此外，在部分信任下运行的网络应用程序（例如具有一组受限的安全权限）不能大于配额大小的一半。

有关如何更改联机应用程序配额的信息和说明，请参阅ClickOnce[概述](../deployment/clickonce-cache-overview.md)。

## <a name="versioning-issues"></a>版本问题

如果将强名称分配给程序集并递增程序集版本号以反映应用程序更新，则可能会遇到问题。 任何使用对强名称程序集的引用编译的程序集都必须自行重新编译，否则程序集将尝试引用旧版本。 程序集将尝试此操作，因为程序集在其绑定请求中使用的是旧版本值。

例如，假设自己的项目中有一个强名称程序集，其版本为 1.0.0.0。 编译程序集后，可将其添加为对包含主应用程序的项目的引用。 如果更新程序集，将版本递增为 1.0.0.1，并尝试在不重新编译应用程序的情况下部署它，则应用程序将无法运行时加载程序集。

只有在手动编辑清单时，才能发生此错误;如果使用 Visual Studio 生成部署， [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 则不应遇到Visual Studio。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>在清单.NET Framework单个程序集

如果已手动编辑部署以引用旧版程序集，则应用程序将无法 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] .NET Framework加载。 例如，如果在清单中指定的 System.Net 版本之前添加了对 System.Net .NET Framework 程序集的引用，则会发生错误。 一般情况下，不应尝试指定对单个 .NET Framework 程序集的引用，因为应用程序运行所针对的 .NET Framework 版本在应用程序清单中指定为依赖项。

## <a name="manifest-parsing-issues"></a>清单分析问题

使用的清单文件是 XML 文件，它们必须格式良好且有效：它们必须遵循 XML 语法规则，并且只能使用相关 XML 架构中定义的元素和 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 属性。

在清单文件中可能会导致问题的内容是选择包含特殊字符（如单引号或双引号）的应用程序的名称。 应用程序的名称是其标识的一 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部分。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 当前不分析包含特殊字符的标识。 如果应用程序无法激活，请确保仅对名称使用字母和数字字符，并尝试再次部署它。

如果已手动编辑部署或应用程序清单，则可能是无意中损坏了这些清单。 损坏的清单将阻止正确 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装。 可以运行时调试此类错误，方法是单击"错误 **ClickOnce"** 对话框上的"详细信息"，并读取日志中的错误消息。 日志将列出以下消息之一：

- 语法错误的说明，以及发生错误的行号和字符位置。

- 违反清单架构使用的元素或属性的名称。 如果已手动将 XML 添加到清单中，必须比较与清单架构的添加内容。 有关详细信息，请参阅部署[ClickOnce清单和](../deployment/clickonce-deployment-manifest.md)ClickOnce[清单](../deployment/clickonce-application-manifest.md)。

- ID 冲突。 部署和应用程序清单中的依赖项引用在它们的 和 属性中必须 `name` `publicKeyToken` 是唯一的。 如果两个属性在清单中的任意两个元素之间匹配，则清单分析将不会成功。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>手动更改清单或应用程序的预防措施

更新应用程序清单时，必须对应用程序清单和部署清单重新签名。 部署清单包含对应用程序清单的引用，其中包括该文件的哈希及其数字签名。

### <a name="precautions-with-deployment-provider-usage"></a>部署提供程序使用情况的预防措施

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署清单具有 一个 属性，该属性指向应安装和服务应用程序的位置的完整 `deploymentProvider` 路径：

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

此路径是在创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序时设置的，并且适用于已安装的应用程序。 路径指向安装程序将安装应用程序的标准位置 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，并搜索更新。 如果使用 **xcopy** 命令将应用程序复制到其他位置，但不更改 属性， 在尝试下载应用程序时仍将引用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `deploymentProvider` [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 回原始位置。

如果要移动或复制应用程序，还必须更新路径，以便客户端 `deploymentProvider` 实际从新位置安装。 如果已安装应用程序，则更新此路径主要是一个问题。 对于始终通过原始 URL 启动的联机应用程序，设置 `deploymentProvider` 是可选的。 如果设置了 ，将采用该 URL;否则，用于启动应用程序的 URL 将用作下载应用程序 `deploymentProvider` 文件的基本 URL。

> [!NOTE]
> 每次更新清单时，还必须再次对清单进行签名。

## <a name="see-also"></a>请参阅

[排ClickOnce部署问题](../deployment/troubleshooting-clickonce-deployments.md) 
[保护ClickOnce应用程序](../deployment/securing-clickonce-applications.md) 
[选择ClickOnce部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
