---
title: 应用程序部署系统必备 | Microsoft Docs
description: 了解应用程序的部署系统必备，包括使用“系统必备”对话框和引导程序包。
ms.custom: SEO-VS-2020
ms.date: 09/23/2021
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: ca078ac6051e4550cd4ec102ccb4a8067675e3fb
ms.sourcegitcommit: 8e74969ff61b609c89b3139434dff5a742c18ff4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2021
ms.locfileid: "128427111"
---
# <a name="application-deployment-prerequisites-windows-desktop"></a>应用程序部署系统必备（Windows 桌面）

若要成功安装和运行 Windows 桌面应用程序，首先将应用程序依赖的所有组件安装到目标计算机上。 例如，使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 创建的大多数应用程序都依赖于 .NET Framework。 在这种情况下，在安装应用程序之前，目标计算机上必须存在正确版本的公共语言运行时。

可在“系统必备”对话框中选择这些系统必备组件，然后在安装过程中安装 .NET Framework 和任何其他可再发行组件。 此做法称为“引导”。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 生成名为 Setup.exe 的 Windows 可执行程序，又称为引导程序。 引导程序负责在运行应用程序之前，安装这些系统必备组件。 有关选择这些系统必备组件的详细信息，请参阅[“系统必备”对话框](../ide/reference/prerequisites-dialog-box.md)。

每个系统必备组件都是一个引导程序包。 一个引导程序包是一组目录和文件，其中包含用于说明系统必备组件的安装方式的清单文件。 如果应用程序的系统必备组件未列在“系统必备组件对话框”中，可以创建自定义引导程序包，将其添加到 Visual Studio。 然后便可在“系统必备组件对话框”中选择这些系统必备组件。 有关详细信息，请参阅[创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

默认情况下，为 Windows Installer 部署（通过使用 Visual Studio 中的安装项目）和 ClickOnce 部署启用引导。 为 Windows Installer 部署生成的引导程序未签名，但在 ClickOnce 部署中，引导程序已签名。 你可以对某个组件禁用引导，但仅当确信所有目标计算机上都已安装该组件的正确版本时，才应这么做。

## <a name="bootstrapping-and-clickonce-deployment"></a>引导和 ClickOnce 部署
 在客户端计算机上安装应用程序之前，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 会对客户端进行检查，以确保客户端具备应用程序清单中指定的要求。 其中包括以下要求：

- 公共语言运行时的最低要求版本（在应用程序清单中被指定为一个程序集依赖项）。

- 应用程序要求的 Windows 操作系统的最低要求版本（在应用程序清单中使用 `<osVersionInfo>` 元素指定）。 （请参阅 [\<dependency> 元素](../deployment/dependency-element-clickonce-application.md)。）

- 必须预先安装在全局程序集缓存 (GAC) 中的所有程序集的最低版本（由程序集清单中的程序集依赖项声明指定）。

  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可以检测到缺少的系统必备组件，并可以使用引导程序安装系统必备组件。 有关详细信息，请参阅[如何：将系统必备组件添加到 ClickOnce 应用程序中](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。

> [!NOTE]
> 若要更改由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和 MageUI.exe 之类的工具生成的清单中的默认值，需要在文本编辑器中编辑应用程序清单，然后对应用程序清单和部署清单重新签名。 有关详细信息，请参阅[如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

 如果你使用 Visual Studio 和 ClickOnce 来部署应用程序，则默认选中的引导程序包取决于解决方案中的 .NET Framework 版本。 但如果更改目标 .NET Framework 版本，则必须手动在“系统必备组件”对话框中更新选项。

|目标 .NET Framework|选中的引导程序包|
|---------------------------|------------------------------------|
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows Installer 3.1|
|.NET Framework 4|.NET Framework 4<br /><br /> Windows Installer 3.1|

 通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 发布向导所生成的 Publish.htm 页指向仅安装应用程序的链接，或指向同时安装应用程序和引导组件的链接。

 如果是使用 Visual Studio 中的 ClickOnce 发布向导或发布页生成的引导程序，则会自动为 Setup.exe 签名。 但如果你希望使用客户的证书为引导程序签名，则可稍后对文件签名。

## <a name="bootstrapping-and-msbuild"></a>引导和 MSBuild
 如果不使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，但是在命令行上编译应用程序，则可以使用 Microsoft 生成引擎 (MSBuild) 任务创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 引导应用程序。 有关详细信息，请参阅 [GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)。

 作为引导的替代方法，你可以使用电子软件分发系统（如 Microsoft Systems Management Server (SMS)）预先部署组件。

## <a name="bootstrapper-setupexe-command-line-arguments"></a>引导程序 (Setup.exe) 命令行参数
 由 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 和 MSBuild 任务生成的 Setup.exe 支持下面一组命令行参数。 任何其他参数都将转发到应用程序安装程序。

 如果更改任何引导程序选项，则必须更改未签名的引导程序，稍后再对引导程序文件进行签名。

| 命令行参数 | 说明 |
| - | - |
| **-h、-?、-Help** | 显示一个“帮助”对话框。 |
| **-url, -componentsurl** | 显示用于此安装的存储 URL 和组件 URL。 |
| **-url=** `location` | 设置 Setup.exe 将在其中查找 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的 URL。 |
| **-componentsurl=** `location` | 设置 Setup.exe 将在其中查找依赖项（如 .NET Framework）的 URL。 |
| **-homesite=** `true` **&#124;** `false` | 如果为 `true`，则从供应商站点上的首选位置下载依赖项。 此设置将重写 -componentsurl 设置。 如果为 `false`，则从 -componentsurl 所指定的 URL 下载依赖项。 |

## <a name="operating-system-support"></a>操作系统支持
 Windows Server 2008 服务器核心或 Windows Server 2008 R2 服务器核心提供功能有限的低级维护服务器环境，不支持 Visual Studio 引导程序。 例如，“服务器核心”安装选项仅支持 .NET Framework 3.5 服务器核心配置文件，它无法运行依赖于完整 .NET Framework 的 Visual Studio 功能。

## <a name="see-also"></a>另请参阅
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)