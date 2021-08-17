---
title: ClickOnce 安全性和部署|Microsoft Docs
description: 了解Visual Studio ClickOnce 的支持，ClickOnce 是一种部署技术，可用于创建基于 Windows 的自更新应用程序。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073898"
---
# <a name="clickonce-security-and-deployment"></a>ClickOnce 安全性和部署
[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 是一种部署技术，可用于创建基于 Windows 的自更新应用程序，这些应用程序可以在最少的用户交互下安装和运行。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 如果已使用 Visual Basic 和 Visual C# 开发项目，则 完全支持发布和更新使用 ClickOnce 技术部署的应用程序。 有关部署应用程序Visual C++，请参阅 [ClickOnce Deployment for Visual C++ Applications](/cpp/windows/clickonce-deployment-for-visual-cpp-applications)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署克服了部署中的三个主要问题：

- **更新应用程序时困难。** 使用 Microsoft Windows Installer部署，每当更新应用程序时，用户都可以安装更新 msp 文件，并应用于已安装的产品;使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署时，可以自动提供更新。 仅下载已更改的应用程序部分，然后从新的并行文件夹中重新安装完整更新的应用程序。

- **对用户计算机的影响。** 使用Windows Installer部署时，应用程序通常依赖于共享组件，并且存在版本控制冲突的可能性;使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署时，每个应用程序都是独立的，不能干扰其他应用程序。

- **安全权限。** Windows Installer部署需要管理权限，并且只允许有限的用户安装; [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署使非管理用户能够安装和仅授予应用程序所需的代码访问安全性权限。

  过去，这些问题有时会导致开发人员决定创建 Web 应用程序而不是基于 Windows 的应用程序，从而牺牲丰富的用户界面以便于安装。 通过使用 部署的应用程序 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ，你可以利用这两种技术。

## <a name="what-is-a-clickonce-application"></a>什么是 ClickOnce 应用程序？
 应用程序是使用技术发布的任何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] *Windows Presentation Foundation (.xbap*) 、Windows 窗体 (*.exe*) 、控制台应用程序 (*.exe*) 或 Office 解决方案 (*.dll* [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]) 。 可以通过三种不同的方式发布应用程序：网页、网络文件共享或 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] CD-ROM 等媒体。 应用程序可以安装在最终用户的计算机上并在本地运行，即使计算机处于脱机状态，也可以以仅联机模式运行，而无需在最终用户的计算机上永久安装任何 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 内容。 有关详细信息，请参阅选择 [ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序可以自我更新;他们可以在更新版本可用时检查它们，并自动替换任何更新的文件。 开发人员可以指定更新行为；网络管理员也可以控制更新策略，如将更新标记为强制性更新。 最终用户或管理员也可以将更新回滚到早期版本。 有关详细信息，请参阅选择 [ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

 由于 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是隔离的，因此安装或运行 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序不能中断现有应用程序。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序是自包含的;每个 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序都安装到每个应用程序的安全缓存中，然后从该缓存运行。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序在 Internet 或 Intranet 安全区域中运行。 必要时，应用程序可以请求提升的安全权限。 有关详细信息，请参阅保护 [ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

## <a name="how-clickonce-security-works"></a>ClickOnce 安全性的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 安全性基于证书、代码访问安全策略和 ClickOnce 信任提示。

### <a name="certificates"></a>证书
 验证码证书用于验证应用程序发布者的真实性。 通过使用 Authenticode 进行应用程序部署，ClickOnce 可帮助防止有害程序将自己视为来自已建立的可信来源的合法程序。 （可选）证书还可用于对应用程序和部署清单进行签名，以证明文件未被篡改。 有关详细信息，请参阅 [ClickOnce 和 Authenticode](../deployment/clickonce-and-authenticode.md)。 证书还可用于将客户端计算机配置为具有受信任的发布者列表。 如果应用程序来自受信任的发布者，则无需用户交互即可安装该应用程序。 有关详细信息，请参阅 [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

### <a name="code-access-security"></a>代码访问安全性
 代码访问安全性有助于限制代码对受保护资源的访问权限。 在大多数情况下，可以选择 Internet 或本地 Intranet 区域来限制权限。 使用 **ProjectDesigner 中的**"安全性"页请求适用于应用程序的区域。 还可以调试具有受限权限的应用程序，以模拟最终用户体验。 有关详细信息，请参阅 [ClickOnce 应用程序的代码访问安全性](../deployment/code-access-security-for-clickonce-applications.md)。

### <a name="clickonce-trust-prompt"></a>ClickOnce 信任提示
 如果应用程序请求的权限超过区域允许的权限，可以提示最终用户做出信任决定。 最终用户可以决定是否信任 ClickOnce 应用程序（Windows 窗体应用程序、Windows Presentation Foundation应用程序、控制台应用程序、XAML 浏览器应用程序和 Office 解决方案）运行。 有关详细信息，请参阅 [如何：配置 ClickOnce 信任提示行为](../deployment/how-to-configure-the-clickonce-trust-prompt-behavior.md)。

## <a name="how-clickonce-deployment-works"></a>ClickOnce 部署的工作原理
 核心 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署体系结构基于两个 XML 清单文件：应用程序清单和部署清单。 这些文件用于描述 ClickOnce 应用程序的安装位置、更新方式和更新时间。

### <a name="publish-clickonce-applications"></a>发布 ClickOnce 应用程序
 应用程序清单描述应用程序本身。 这包括程序集、创建应用程序的依赖项和文件、所需的权限以及更新可用的位置。 应用程序开发人员通过使用 Visual Studio 中的发布向导或 *清单生成和编辑工具 (Mage.exe)* 创建应用程序 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 清单。 有关详细信息，请参阅 [如何：使用发布](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)向导 发布 ClickOnce 应用程序。

 部署清单描述应用程序的部署方式。 这包括应用程序清单的位置以及客户端应运行的应用程序版本。

### <a name="deploy-clickonce-applications"></a>部署 ClickOnce 应用程序
 创建部署清单后，部署清单将复制到部署位置。 该位置可以是 Web 服务器、网络文件共享或媒体（如 CD）。 应用程序清单和所有应用程序文件也会复制到部署清单中指定的部署位置。 该位置可以与部署清单的部署位置相同，也可以不同。 在 Visual Studio向导时，将自动执行复制操作。

### <a name="install-clickonce-applications"></a>安装 ClickOnce 应用程序
 部署到部署位置后，最终用户可以通过单击表示网页或文件夹中的部署清单文件的图标来下载并安装应用程序。 在大多数情况下，向最终用户显示一个简单的对话框，要求用户确认安装，之后安装继续进行，应用程序无需额外的干预即可启动。 如果应用程序需要提升的权限，或者应用程序未由受信任的证书签名，则对话框还会要求用户授予权限，然后才能继续安装。 尽管 ClickOnce 安装是按用户安装的，但如果存在需要管理员权限的先决条件，可能需要权限提升。 有关提升的权限详细信息，请参阅 [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)。

 证书可以在计算机或企业级别受信任，以便使用受信任的证书签名的 ClickOnce 应用程序可以无提示安装。 有关受信任的证书详细信息，请参阅 [受信任的应用程序部署概述](../deployment/trusted-application-deployment-overview.md)。

 可以将应用程序添加到用户的"开始"菜单和"添加或删除程序"组 **，控制面板。** 与其他部署技术不同，不会向 **Program Files** 文件夹或注册表添加任何内容，并且无需管理权限进行安装

> [!NOTE]
> 还可以阻止将应用程序添加到"开始"菜单和"添加或删除程序"组，实际上使其行为类似于 Web 应用程序。 有关详细信息，请参阅选择 [ClickOnce 部署策略](../deployment/choosing-a-clickonce-deployment-strategy.md)。

### <a name="update-clickonce-applications"></a>更新 ClickOnce 应用程序
 当应用程序开发人员创建应用程序的更新版本时，他们生成新的应用程序清单，将文件复制到部署位置-通常是原始应用程序部署文件夹的同级文件夹。 管理员更新部署清单，以指向新版本应用程序的位置。

> [!NOTE]
> 可以使用 **Visual Studio** 向导执行这些步骤。

 除了部署位置之外，部署清单还包含一个更新 (位于应用程序检查更新) 的网页或网络文件共享中。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]**"** 发布"属性用于指定应用程序检查更新的"时间"和"时间"。 可以在部署清单中指定更新行为，或者可以通过 API 在应用程序的用户界面中将更新行为呈现为用户 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 选择。 此外，Publish 属性还可用于将更新设置为强制执行，或用于将应用程序回滚到较早版本。 有关详细信息，请参阅选择 [ClickOnce 更新策略](../deployment/choosing-a-clickonce-update-strategy.md)。

### <a name="third-party-installers"></a>第三方安装程序
 可以自定义 ClickOnce 安装程序，以连同应用程序一起安装第三方组件。 你必须将可再发行 (.exe包.msi文件) 使用非特定语言产品清单和特定于语言的包清单描述包。 有关详细信息，请参阅创建 [引导程序包](../deployment/creating-bootstrapper-packages.md)。

## <a name="clickonce-tools"></a>ClickOnce 工具
 下表显示了可用于生成、编辑、签名和重新签名应用程序和部署清单的工具。

|工具|说明|
|----------|-----------------|
|[”项目设计器“ -&gt;“安全”页](../ide/reference/security-page-project-designer.md)|对应用程序和部署清单进行签署。|
|[“项目设计器”-&gt;“发布”页](../ide/reference/publish-page-project-designer.md)|为 Visual Basic 和 Visual C# 应用程序生成和编辑应用程序和部署清单。|
|[*Mage.exe(清单生成和编辑工具)*](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)|为 Visual Basic、Visual C# 和 Visual C++ 生成应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签署和重新签署。<br /><br /> 可以从批处理脚本和命令提示符运行。|
|[*MageUI.exe(清单生成和编辑工具，* 图形客户端)](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)|生成和编辑应用程序和部署清单。<br /><br /> 对应用程序和部署清单进行签署和重新签署。|
|[GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)|生成应用程序清单。<br /><br /> 可以从 MSBuild。 有关详细信息，请参阅 MSBuild[引用](../msbuild/msbuild-reference.md)。|
|[GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)|生成部署清单。<br /><br /> 可以从 MSBuild。 有关详细信息，请参阅 MSBuild[引用](../msbuild/msbuild-reference.md)。|
|[SignFile 任务](../msbuild/signfile-task.md)|对应用程序和部署清单进行签署。<br /><br /> 可以从 MSBuild。 有关详细信息，请参阅 MSBuild[引用](../msbuild/msbuild-reference.md)。|
|[Microsoft.Build.Tasks.Deployment.ManifestUtilities](/dotnet/api/microsoft.build.tasks.deployment.manifestutilities)|开发自己的应用程序以生成应用程序和部署清单。|

 下表显示了支持这些.NET Framework应用程序所需的ClickOnce版本。

|浏览者|.NET Framework 版本|
|-------------|----------------------------|
|Internet Explorer|2.0、3.0、3.5、3.5 SP1、4|
|Firefox|2.0 SP1、3.5 SP1、4|
|Chrome|3.5|
|Microsoft Edge|3.5|

## <a name="see-also"></a>请参阅
- [Windows Vista 上的 ClickOnce 部署](../deployment/clickonce-deployment-on-windows-vista.md)
- [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)
- [保护 ClickOnce 应用程序](../deployment/securing-clickonce-applications.md)
- [使用 ClickOnce 部署 COM 组件](../deployment/deploying-com-components-with-clickonce.md)
- [从命令行生成 ClickOnce 应用程序](../deployment/building-clickonce-applications-from-the-command-line.md)
- [调试ClickOnce System.Deployment.Application 的应用程序](../deployment/debugging-clickonce-applications-that-use-system-deployment-application.md)
