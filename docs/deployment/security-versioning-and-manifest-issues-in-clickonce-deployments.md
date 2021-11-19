---
title: 安全/版本控制/清单问题 (ClickOnce)
description: 了解可能导致 ClickOnce 部署失败的关于 ClickOnce 安全、应用程序版本控制和清单语法和语义的问题。
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665462"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 部署中的安全、版本控制和清单问题

存在各种关于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安全、应用程序版本控制和清单语法和语义的问题，这些问题可能导致 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署失败。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce 和 Windows Vista 用户帐户控制

在 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 中，应用程序默认以标准用户身份运行，即使当前用户使用具有管理员权限的帐户登录。 如果应用程序必须执行需要管理员权限的操作，它会告知操作系统，然后系统会提示用户输入其管理员凭据。 此功能称为用户帐户控制 (UAC)，可防止应用程序在未经用户明确批准的情况下做出可能影响整个操作系统的更改。 Windows 应用程序通过在其应用程序清单的 `trustInfo` 部分中指定 `requestedExecutionLevel` 属性来声明其需要此权限提升。

由于存在将应用程序暴露于安全提升攻击的风险，因此，如果为客户端启用了 UAC，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序无法请求权限提升。 尝试将其 `requestedExecutionLevel` 属性设置为 `requireAdministrator` 或 `highestAvailable` 的任何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序将不会安装在 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 上。

在某些情况下，由于 [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 上的安装程序检测逻辑，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可能尝试使用管理员权限运行。 在这种情况下，可以将应用程序清单中的 `requestedExecutionLevel` 属性设置为 `asInvoker`。 这会使应用程序本身在没有提升的情况下运行。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] 会自动将此属性添加到所有应用程序清单。

如果要开发的应用程序需要在应用程序的整个生存期内具有管理员权限，则应考虑改为使用 Windows Installer (MSI) 技术部署应用程序。 有关详细信息，请参阅 [Windows Installer 基础知识](../extensibility/internals/windows-installer-basics.md)。

## <a name="online-application-quotas-and-partial-trust-applications"></a>联机应用程序配额和部分可信的应用程序

如果 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序联机运行而不是通过安装运行，则该应用程序必须位于为联机应用程序保留的配额范围内。 此外，在部分信任情况下运行的网络应用程序（例如具有一组受限的安全权限）不能大于配额大小的一半。

有关详细信息和有关如何更改联机应用程序配额的说明，请参阅 [ClickOnce 缓存概述](../deployment/clickonce-cache-overview.md)。

## <a name="versioning-issues"></a>版本问题

如果将强名称分配给程序集并递增程序集版本号以反映应用程序更新，则可能会出现问题。 使用具有强名称的程序集的引用编译的任何程序集都必须自行重新编译，否则程序集将尝试引用较旧的版本。 程序集将尝试此操作，因为它在其绑定请求中使用的是旧版本值。

例如，假设项目中有一个具有强名称的程序集，其版本为 1.0.0.0。 编译程序集后，可将其添加为对包含主应用程序的项目的引用。 如果需更新程序集，将版本增加到 1.0.0.1，并尝试在无需重新编译应用程序的情况下部署它，则应用程序将无法在运行时加载程序集。

只有在手动编辑 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单时，才会出现此错误；如果使用 Visual Studio 生成部署，则不应出现此错误。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>在清单中指定单个 .NET Framework 程序集

如果已手动编辑 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署以引用 .NET Framework 程序集的较旧版本，则应用程序将无法加载。 例如，如果为清单中指定版本之前的 .NET Framework 版本添加了 System.Net 程序集引用，则会出现错误。 通常，不应尝试指定对单个 .NET Framework 程序集的引用，因为应用程序针对其运行的 .NET Framework 版本在应用程序清单中指定为依赖项。

## <a name="manifest-parsing-issues"></a>清单分析问题

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 使用的清单文件是 XML 文件，这些文件必须格式标准且有效：它们必须遵守 XML 语法规则，并且只能使用相关 XML 架构中定义的元素和属性。

在清单文件中可能导致问题的操作是为应用程序选择包含特殊字符（如单引号或双引号）的名称。 应用程序的名称是其 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 标识的一部分。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 当前不分析包含特殊字符的标识。 如果应用程序无法激活，请确保仅在名称中使用字母和数字字符，然后尝试再次对其进行部署。

如果你手动编辑了部署或应用程序清单，则可能是无意中损坏了这些清单。 已损坏的清单将阻止正确的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装。 可在运行时调试此类错误，方法是通过单击“ClickOnce 错误”对话框中的“详细信息”，并阅读日志中的错误消息 。 日志将列出以下消息之一：

- 语法错误的描述，以及发生错误的行号和字符位置。

- 所使用的违反清单架构的元素或属性的名称。 如果已手动将 XML 添加到清单中，则必须将添加的内容与清单架构进行比较。 有关详细信息，请参阅 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)和 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)。

- ID 冲突。 部署和应用程序清单中的依赖项引用在其 `name` 和 `publicKeyToken` 属性中必须是唯一的。 如果两个属性均与清单中的任意两个元素匹配，则清单分析将失败。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>手动更改清单或应用程序时的注意事项

更新应用程序清单时，必须对应用程序清单和部署清单进行重新签名。 部署清单包含对应用程序清单的引用，其中包括该文件的哈希及其数字签名。

### <a name="precautions-with-deployment-provider-usage"></a>使用部署提供程序的注意事项

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单具有一个 `deploymentProvider` 属性，该属性指向应安装应用程序和为应用程序提供服务的位置的完整路径：

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

此路径是在 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 创建应用程序时设置的，对于已安装的应用程序是必需的。 此路径指向 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安装程序将从中安装应用程序并搜索更新的标准位置。 如果使用 xcopy 命令将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序复制到其他位置，但不更改 `deploymentProvider` 属性，则 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 在尝试下载应用程序时仍将引用原始位置。

如果要移动或复制应用程序，还必须更新 `deploymentProvider` 路径，以便客户端实际上从新位置进行安装。 如果已安装应用程序，则更新此路径在大多数时候都会成为一个问题。 对于始终通过原始 URL 启动的联机应用程序，可选择设置 `deploymentProvider`。 如果设置了 `deploymentProvider`，则将使用该 URL；否则，将使用用于启动应用程序的 URL 作为下载应用程序文件的基 URL。

> [!NOTE]
> 每次更新清单时，还必须再次对其进行签名。

## <a name="see-also"></a>另请参阅

[ClickOnce 部署故障排除](../deployment/troubleshooting-clickonce-deployments.md)
[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
