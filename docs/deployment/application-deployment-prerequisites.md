---
title: 应用程序部署先决条件|Microsoft Docs
description: 了解应用程序的部署先决条件，包括使用"先决条件"对话框和引导程序包。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
ms.openlocfilehash: cdf5e873996f27c1ac56e7148dbea2aea491030c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160954"
---
# <a name="application-deployment-prerequisites"></a>应用程序部署必备

若要使应用程序成功安装和运行，请首先安装应用程序依赖目标计算机的所有组件。 例如，使用 创建的大多数 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 应用程序都依赖于.NET Framework。 在这种情况下，在安装应用程序之前，目标计算机上必须存在公共语言运行时的正确版本。

 可以在"先决条件"对话框中选择这些先决条件，.NET Framework安装组件和任何其他可再发行组件。 此做法称为“引导”。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]生成名为 Windows 的可执行 *Setup.exe* 程序，也称为 *引导程序*。 引导程序负责在运行应用程序之前，安装这些系统必备组件。 有关选择这些先决条件的详细信息，请参阅 [先决条件对话框](../ide/reference/prerequisites-dialog-box.md)。

 每个系统必备组件都是一个引导程序包。 引导程序包是一组目录和文件，其中包含描述如何安装先决条件的清单文件。 如果应用程序的系统必备组件未列在“系统必备组件对话框”中，可以创建自定义引导程序包，将其添加到 Visual Studio。 然后便可在“系统必备组件对话框”中选择这些系统必备组件。 有关详细信息，请参阅 [创建引导程序包](../deployment/creating-bootstrapper-packages.md)。

 默认情况下，ClickOnce 部署可以使用引导。 对为 ClickOnce 部署生成的引导程序进行签名。 可以禁用组件的启动，但仅在确定组件的正确版本已安装在所有目标计算机上时。

## <a name="bootstrapping-and-clickonce-deployment"></a>引导和 ClickOnce 部署
 在客户端计算机上安装应用程序之前，请检查客户端 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 以确保其满足应用程序清单中指定的要求。 其中包括以下要求：

- 公共语言运行时的最低要求版本（在应用程序清单中被指定为一个程序集依赖项）。

- 应用程序要求的 Windows 操作系统的最低要求版本（在应用程序清单中使用 `<osVersionInfo>` 元素指定）。  ([ \<dependency> 元素](../deployment/dependency-element-clickonce-application.md).) 

- 必须在全局程序集缓存 (GAC) 预安装的所有程序集的最低版本，如程序集清单中的程序集依赖项声明所指定。

  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可以检测缺少的先决条件，并且可以使用引导程序安装必备组件。 有关详细信息，请参阅[如何：使用应用程序安装ClickOnce必备组件](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)。

> [!NOTE]
> 若要更改由 和MageUI.exe等工具生成的清单中的值，需要在文本编辑器中编辑应用程序清单，然后对应用程序和部署清单重新签名 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 ** 有关详细信息，请参阅[如何：对应用程序和部署清单重新签名](../deployment/how-to-re-sign-application-and-deployment-manifests.md)。

 如果你使用 Visual Studio 和 ClickOnce 来部署应用程序，则默认选中的引导程序包取决于解决方案中的 .NET Framework 版本。 但如果更改目标 .NET Framework 版本，则必须手动在“系统必备组件”对话框中更新选项。

|目标 .NET Framework|选中的引导程序包|
|---------------------------|------------------------------------|
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows Installer 3.1|
|.NET Framework 4|.NET Framework 4<br /><br /> Windows Installer 3.1|

 借助部署，Publish.htm向导生成的"部署"页指向仅安装应用程序的链接，或指向同时安装应用程序和启动 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]  [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 组件的链接。

 如果是使用 Visual Studio 中的 ClickOnce 发布向导或发布页生成的引导程序，则会自动为 Setup.exe 签名。 但如果你希望使用客户的证书为引导程序签名，则可稍后对文件签名。

## <a name="bootstrapping-and-msbuild"></a>引导和 MSBuild
 如果不使用 ，而是在命令行上编译应用程序，则可以通过使用 Microsoft 生成引擎 (MSBuild) [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 有关详细信息，请参阅 [GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)。

 作为引导的替代方法，你可以使用电子软件分发系统（如 Microsoft Systems Management Server (SMS)）预先部署组件。

## <a name="bootstrapper-setupexe-command-line-arguments"></a>引导程序 (Setup.exe) 命令行参数
 和 *MSBuild* 任务生成的Setup.exe[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 支持以下一组命令行参数。 任何其他参数将转发到应用程序安装程序。

 如果更改任何引导程序选项，则必须更改未签名的引导程序，然后对引导程序文件进行签名。

| 命令行参数 | 说明 |
| - | - |
| **-h、-?、-Help** | 显示一个“帮助”对话框。 |
| **-url, -componentsurl** | 显示用于此安装的存储 URL 和组件 URL。 |
| **-url=**`location` | 设置应用程序 *Setup.exe* 的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] URL。 |
| **-componentsurl=** `location` | 设置要查找 *Setup.exe* 的 URL，例如.NET Framework。 |
| **-homesite=** `true`**&#124;**`false` | 如果 `true` 为 ，则从供应商站点上的首选位置下载依赖项。 此设置替代 **-componentsurl** 设置。 当 `false` 为 时，从 **-componentsurl 指定的** URL 下载依赖项。 |

## <a name="operating-system-support"></a>操作系统支持
 Windows Server 2008 Server Core 或 Windows Server 2008 R2 Server Core 不支持 Visual Studio 引导程序，因为它们提供低维护服务器环境，功能有限。 例如，Server Core 安装选项仅支持 .NET Framework 3.5 Server Core 配置文件，该配置文件无法运行依赖于完整 Visual Studio 的 .NET Framework。

## <a name="see-also"></a>请参阅
- [选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)