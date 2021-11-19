---
title: ClickOnce 安全性和部署 | Microsoft Docs
description: 了解 Visual Studio 对 ClickOnce 的支持，ClickOnce 是一种部署技术，可用于创建基于 Windows 的自我更新应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce deployment
- deploying applications [ClickOnce]
- ClickOnce deployment
- publishing, ClickOnce
ms.assetid: abab6d34-c3c2-45c1-a8b6-43c7d3131e7a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 264dcfd427b70c452a86caee4fc20c3421a4e9aa
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671820"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce 安全性和部署
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 是一种部署技术，可用于创建基于 Windows 的自我更新应用程序，这些应用程序安装和运行时可将用户交互降至最低。 如果使用 Visual Basic 和 Visual C# 开发了项目，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将为发布和更新使用 ClickOnce 技术部署的应用程序提供全面支持。 若要了解如何部署 Visual C++ 应用程序，请参阅 [Visual C++ 应用程序的 ClickOnce 部署](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署克服了部署中的 3 个主要问题：

- **更新应用程序时遇到的困难。** 使用 Microsoft Windows Installer 部署，每当应用程序更新时，用户都可安装更新和 msp 文件，并将其应用于已安装的产品；而使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署，你可自动提供更新。 只会下载应用程序已更改的部分，然后从新的并行文件夹中重新安装完整的、更新后的应用程序。

- **对用户计算机的影响。** 使用 Windows Installer 部署时，应用程序通常依赖于共享组件，可能会导致版本控制冲突；而使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署时，每个应用程序都是独立的，不能干扰其他应用程序。

- **安全权限。** Windows Installer 部署需要管理权限，并且仅允许有限的用户安装；[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署使非管理用户也能进行安装，并仅授予应用程序所需的代码访问安全性权限。

  过去，这些问题有时会导致开发人员决定创建 Web 应用程序而不是基于 Windows 的应用程序，为了便于安装而牺牲了丰富的用户界面。 通过使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署的应用程序，你可获得这两种技术的优势。

## <a name="what-is-a-clickonce-application"></a>什么是 ClickOnce 应用程序？
 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 技术发布的任何 Windows Presentation Foundation (.xbap)、Windows 窗体 (.exe)、控制台应用程序 (.exe) 或 Office 解决方案 (.dll)   。 可通过 3 种不同的方式发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序：通过网页、通过网络文件共享或通过媒体（如 CD-ROM）发布。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可安装在最终用户的计算机上，甚至在计算机脱机时也可在本地运行，它也可在仅联机模式下运行，而无需在最终用户的计算机上永久安装任何内容。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可自我更新；它们可检查是否有更新版本可用，并自动替换所有已更新的文件。 开发人员可以指定更新行为；网络管理员也可以控制更新策略，如将更新标记为强制性更新。 最终用户或管理员还可将更新回滚到早期版本。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是独立的，因此安装或运行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序不会中断现有应用程序。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是独立的；每个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序都安装到安全的每用户、每应用程序缓存中并从这里运行。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序在 Internet 或 Intranet 安全区域中运行。 必要时，应用程序可以请求提升的安全权限。 有关详细信息，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

## <a name="how-clickonce-security-works"></a>ClickOnce 安全的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安全基于证书、代码访问安全性策略和 ClickOnce 信任提示。

### <a name="certificates"></a>证书
 验证码证书用于验证应用程序发布者的真实性。 通过使用验证码进行应用程序部署，ClickOnce 有助于防止有害程序将自己伪装成来自经证实的、值得信赖的来源的合法程序。 另外，还可使用证书对应用程序和部署清单进行签名，以证明文件未被篡改。 有关详细信息，请参阅 [ClickOnce 和验证码](../deployment/clickonce-and-authenticode.md)。 证书还可用于配置客户端计算机，使其拥有受信任的发布者的列表。 如果某个应用程序来自受信任的发布者，则可在没有任何用户交互的情况下安装它。 有关详细信息，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

### <a name="code-access-security"></a>代码访问安全性
 代码访问安全性可帮助限制代码对受保护资源的访问权限。 在大多数情况下，你可选择 Internet 或本地 Intranet 区域来限制权限。 使用 ProjectDesigner 中的“安全性”页面来请求适合应用程序的区域 。 你还可使用受限权限调试应用程序，来模拟最终用户体验。 有关详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。

### <a name="clickonce-trust-prompt"></a>ClickOnce 信任提示
 如果应用程序请求的权限超过区域允许的权限，则系统会提示最终用户进行信任决定。 最终用户可决定是否信任 ClickOnce 应用程序运行，这些应用包括 Windows 窗体应用程序、Windows Presentation Foundation 应用程序、控制台应用程序、XAML 浏览器应用程序和 Office 解决方案。 有关详细信息，请参阅[如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="how-clickonce-deployment-works"></a>ClickOnce 部署的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署体系结构基于两个 XML 清单文件，它们是应用程序清单和部署清单。 这些文件用于描述从哪里安装 ClickOnce 应用程序、如何更新这些应用程序以及何时更新它们。

### <a name="publish-clickonce-applications"></a>发布 ClickOnce 应用程序
 应用程序清单描述应用程序本身。 其中包括程序集、构成应用程序的依赖项和文件、所需的权限以及提供更新的位置。 应用程序开发人员使用 Visual Studio 中的“发布向导”或 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 中的清单生成和编辑工具 (Mage.exe) 来创建应用程序清单。 有关详细信息，请参阅[如何：使用发布向导发布 ClickOnce 应用程序](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)。

 部署清单描述应用程序的部署方式。 其中包括应用程序清单的位置和客户端应运行的应用程序版本。

### <a name="deploy-clickonce-applications"></a>部署 ClickOnce 应用程序
 创建后，部署清单会复制到部署位置。 该位置可以是 Web 服务器、网络文件共享或媒体（如 CD）。 应用程序清单和所有应用程序文件也会复制到部署清单中指定的部署位置。 该位置可以与部署清单的部署位置相同，也可以不同。 在 Visual Studio 中使用“发布向导”时，会自动执行复制操作。

### <a name="install-clickonce-applications"></a>安装 ClickOnce 应用程序
 在将其部署到部署位置后，最终用户可单击网页或文件夹中表示部署清单文件的图标来下载和安装应用程序。 在大多数情况下，最终用户会看到一个简单的对话框，它要求用户确认安装，然后继续安装，无需额外干预即会启动应用程序。 如果应用程序需要提升的权限，或应用程序未使用受信任的证书进行签名，则对话框还会要求用户授予权限，然后才能继续安装。 尽管 ClickOnce 安装按每位用户进行，但如果先决条件要求具备管理员权限，则可能需要权限提升。 若要详细了解提升的权限，请参阅[保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

 证书可在计算机或企业级别受到信任，以便使用受信任的证书签名的 ClickOnce 应用程序可在无提示的情况下进行安装。 若要详细了解受信任的证书，请参阅[受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

 可将应用程序添加到用户的“开始”菜单中和“控制面板”的“添加或删除程序”组中  。 不同于其他部署技术，不会有任何内容添加到“程序文件”文件夹或注册表，并且无需管理权限即可安装

> [!NOTE]
> 也可阻止将应用程序添加到“开始”菜单和“添加或删除程序”组，从而使其行为与 Web 应用程序类似 。 有关详细信息，请参阅[选择 ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

### <a name="update-clickonce-applications"></a>更新 ClickOnce 应用程序
 应用程序开发人员创建应用程序的更新版本时，会生成新的应用程序清单，并将文件复制到部署位置（通常是原始应用程序部署文件夹的同级文件夹）。 管理员会更新部署清单，使其指向应用程序新版本的位置。

> [!NOTE]
> 可使用 Visual Studio 中的“发布向导”来执行这些步骤。

 除了部署位置之外，部署清单还包含一个更新位置（网页或网络文件共享），应用程序在这里检查更新版本。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 的 Publish 属性用于指定应用程序检查更新的时间和频率。 可在部署清单中指定更新行为，也可通过 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] API 在应用程序的用户界面上以用户选择的方式呈现。 此外，Publish 属性还可用于将更新设置为强制执行，或用于将应用程序回滚到较早版本。 有关详细信息，请参阅[选择 ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

### <a name="third-party-installers"></a>第三方安装程序
 可自定义 ClickOnce 安装程序，以便随应用程序一起安装第三方组件。 必须拥有可再发行包（.exe 或 .msi 文件），并使用中性语言产品清单和特定语言包清单来描述该包。 有关详细信息，请参阅[创建 Bootstrapper包](../deployment/creating-bootstrapper-packages.md)。

## <a name="clickonce-tools"></a>ClickOnce 工具
 下表显示了可用于对应用程序和部署清单进行生成、编辑、签名和重新签名的工具。

|工具|说明|
|----------|-----------------|
|[”项目设计器“ -&gt;“安全”页](../ide/reference/security-page-project-designer.md)|对应用程序和部署清单进行签名。|
|[“项目设计器”-&gt;“发布”页](../ide/reference/publish-page-project-designer.md)|为 Visual Basic 和 Visual C# 应用程序生成和编辑应用程序和部署清单。|
|[*Mage.exe*（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|为 Visual Basic、Visual C# 和 Visual C++ 应用程序生成应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签名和重新签名。<br /><br /> 可从批处理脚本和命令提示符运行。|
|[*MageUI.exe*（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|生成和编辑应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签名和重新签名。|
|[GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)|生成应用程序清单。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|
|[GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)|生成部署清单。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|
|[SignFile 任务](../msbuild/signfile-task.md)|对应用程序和部署清单进行签名。<br /><br /> 可从 MSBuild 运行。 有关详细信息，请参阅 [MSBuild 参考](../msbuild/msbuild-reference.md)。|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|开发自己的应用程序，以生成应用程序和部署清单。|

 下表显示了在以下浏览器中支持 ClickOnce 应用程序所需的 .NET Framework 版本。

|浏览者|.NET Framework 版本|
|-------------|----------------------------|
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|
|Firefox|2.0 SP1、3.5 SP1、4|
|Chrome|3.5|
|Microsoft Edge|3.5|

## <a name="see-also"></a>另请参阅
- [Windows Vista 上的 ClickOnce 部署](../deployment/clickonce-deployment-on-windows-vista.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [使用 ClickOnce 部署 COM 组件](../deployment/deploying-com-components-with-clickonce.md)
- [从命令行生成 ClickOnce 应用程序](../deployment/building-clickonce-applications-from-the-command-line.md)
- [调试使用 System.Deployment.Application 的 ClickOnce 应用程序](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
