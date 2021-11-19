---
title: 从命令行生成 ClickOnce 应用程序 | Microsoft Docs
description: 了解如何从命令行生成 Visual Studio 项目，以便可以使用自动化过程重现生成。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, from command line
- publishing
- publishing, ClickOnce
ms.assetid: d9bc6212-c584-4f72-88c9-9a4b998c555e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: 6bb7d455bf85ef9ba1776956330ac217b73cd2dd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126671833"
---
# <a name="build-clickonce-applications-from-the-command-line"></a>从命令行生成 ClickOnce 应用程序

在 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 中，可以从命令行生成项目，即使它们是在集成开发环境 (IDE) 中创建的。 事实上，可以在另一台仅安装了 .NET Framework 的计算机上重新生成使用 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 创建的项目。 这样就可以使用自动化过程（例如在中心生成实验室）或超出生成项目本身范围的高级脚本编写技术来重现生成。

## <a name="use-msbuild-to-reproduce-net-framework-clickonce-application-deployments"></a>使用 MSBuild 重现 .NET Framework ClickOnce 应用程序部署

 在命令行调用 msbuild /target:publish 时，该命令行将指示 MSBuild 系统生成项目并在发布文件夹中创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序。 这相当于在 IDE 中选择“发布”命令。

 此命令执行位于 Visual Studio 命令提示符环境中路径上的 msbuild.exe。

 “目标”是指示 MSBuild 如何处理命令的指示器。 关键目标是“生成”目标和“发布”目标。 生成目标相当于在 IDE 中选择“生成”命令（或按 F5）。 如果只需生成项目，可以通过键入 `msbuild` 来实现。 此命令有效，因为生成目标是由 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] 生成的所有项目的默认目标。 这意味着不需要明确指定生成目标。 因此，键入 `msbuild` 与键入 `msbuild /target:build` 是相同的操作。

 `/target:publish` 命令指示 MSBuild 调用发布目标。 发布目标取决于生成目标。 这意味着发布操作是生成操作的超集。 例如，如果对其中某个 Visual Basic 或 C# 源文件进行了更改，则发布操作将自动重新生成相应的程序集。

 有关如何使用 Mage.exe 命令行工具生成完整 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署以创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单的信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="create-and-build-a-basic-clickonce-application-with-msbuild"></a>使用 MSBuild 创建和生成基本的 ClickOnce 应用程序

### <a name="to-create-and-publish-a-clickonce-project"></a>创建和发布 ClickOnce 项目

1. 打开 Visual Studio 并创建一个新项目。

    选择“Windows 桌面应用程序”项目模板并将项目命名为 `CmdLineDemo`。

1. 从“生成”菜单中，单击“发布”命令 。

    此步骤可确保正确配置项目以生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署。

    出现“发布向导”。

1. 在“发布”向导中，选择“完成”。

    Visual Studio 生成并显示名为 Publish.htm 的默认网页。

1. 保存项目，并记下存储该项目的文件夹位置。

   上述步骤创建了一个首次发布的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 项目。 现在可以在 IDE 之外重现生成。

#### <a name="to-reproduce-the-build-from-the-command-line"></a>从命令行重现生成

1. 退出 [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)]。

2. 从 Windows“开始”菜单，依次单击“所有程序”、“Microsoft Visual Studio”、“Visual Studio Tools”、“Visual Studio 命令提示符”    。 这应会在当前用户的根文件夹中打开命令提示符。

3. 在“Visual Studio 命令提示符”中，将当前目录更改为在上面刚刚生成的项目的位置。 例如，键入 `chdir My Documents\Visual Studio\Projects\CmdLineDemo`。

4. 若要删除“创建和发布 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 项目”中生成的现有文件，请键入 `rmdir /s publish`。

    此步骤是可选的，但它可确保新文件均由命令行生成而生成。

5. 键入 `msbuild /target:publish`。

   上述步骤将在名为 Publish 的项目子文件夹中生成完整的 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署。 CmdLineDemo.application 是 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署清单。 文件夹 CmdLineDemo_1.0.0.0 包含文件 CmdLineDemo.exe 和 CmdLineDemo.exe.manifest（即 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单）  。 Setup.exe 是引导程序，默认配置为安装 .NET Framework。 DotNetFX 文件夹包含 .NET Framework 的可再发行组件。 这是通过 Web、UNC 或 CD/DVD 部署应用程序所需的整个文件集。

> [!NOTE]
> MSBuild 系统使用 PublishDir 选项指定输出位置，例如 `msbuild /t:publish /p:PublishDir="<specific location>"`。

::: moniker range=">=vs-2019"

## <a name="build-net-clickonce-applications-from-the-command-line"></a>从命令行生成 .NET ClickOnce 应用程序

从命令行生成 .NET ClickOnce 应用程序的过程相似，不同之处在于需要在 MSBuild 命令行上为发布配置文件提供其他属性。 创建发布配置文件的最简单方法是使用 Visual Studio。  有关详细信息，请参阅[使用 ClickOnce 部署 .NET Windows 应用程序](quickstart-deploy-using-clickonce-folder.md)。

创建发布配置文件后，可以在 msbuild 命令行上提供 pubxml 文件作为属性。 例如：

```cmd
    msbuild /t:publish /p:PublishProfile=<pubxml file> /p:PublishDir="<specific location>"
```
::: moniker-end

## <a name="publish-properties"></a>发布属性

 在上述过程中发布应用程序时，以下属性将通过“发布”向导插入到项目文件中，或者插入到 .NET Core 3.1 或更高版本项目的发布配置文件中。 这些属性直接影响 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的生成方式。

 在 CmdLineDemo.vbproj / CmdLineDemo.csproj 中 ：

```xml
<AssemblyOriginatorKeyFile>WindowsApplication3.snk</AssemblyOriginatorKeyFile>
<GenerateManifests>true</GenerateManifests>
<TargetZone>LocalIntranet</TargetZone>
<PublisherName>Microsoft</PublisherName>
<ProductName>CmdLineDemo</ProductName>
<PublishUrl>http://localhost/CmdLineDemo</PublishUrl>
<Install>true</Install>
<ApplicationVersion>1.0.0.*</ApplicationVersion>
<ApplicationRevision>1</ApplicationRevision>
<UpdateEnabled>true</UpdateEnabled>
<UpdateRequired>false</UpdateRequired>
<UpdateMode>Foreground</UpdateMode>
<UpdateInterval>7</UpdateInterval>
<UpdateIntervalUnits>Days</UpdateIntervalUnits>
<UpdateUrlEnabled>false</UpdateUrlEnabled>
<IsWebBootstrapper>true</IsWebBootstrapper>
<BootstrapperEnabled>true</BootstrapperEnabled>
```

 对于 .NET Framework 项目，可在命令行中替代任何这些属性，而无需更改项目文件本身。 例如，以下命令将在没有引导程序的情况下生成 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序部署：

```cmd
msbuild /target:publish /property:BootstrapperEnabled=false
 ```

::: moniker range=">=vs-2019"
对于 .NET Core 3.1 或更高版本，这些项目设置在 pubxml 文件中提供。

 发布属性在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中通过“项目设计器”的“发布”、“安全性”和“签名”属性页控制   。 下面是发布属性的说明，以及如何在应用程序设计器的各种属性页面中设置每个属性的指示：

> [!NOTE]
> 对于 .NET Windows 桌面项目，现在可以在“发布”向导中找到这些设置
::: moniker-end

- `AssemblyOriginatorKeyFile` 确定用于对 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单进行签名的密钥文件。 也可使用此同一密钥为程序集分配一个强名称。 此属性是在“项目设计器”的“签名”页面上设置的 。
::: moniker range=">=vs-2019"
对于 .NET windows 应用程序，此设置保留在项目文件中
::: moniker-end

  在“安全性”页上设置了以下属性：

- “启用 ClickOnce 安全性设置”确定是否生成了 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单。 最初创建项目时，[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 清单生成默认处于关闭状态。 向导会在首次发布时自动打开此标志。

- TargetZone 确定要发送到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中的信任级别。 可能的值为“Internet”、“LocalIntranet”和“自定义”。 Internet 和 LocalIntranet 会导致将默认权限集发送到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单。 LocalIntranet 是默认值，它基本上意味着完全信任。 自定义指定仅将基本 app.manifest 文件中显式指定的权限发送到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中。 app.manifest 文件是仅包含信任信息定义的部分清单文件。 它是一个隐藏文件，当在“安全性”页面上配置权限时，它将自动添加到项目中。
-
::: moniker range=">=vs-2019"
> [!NOTE]
> 对于 .NET Core 3.1 或更高版本的 Windows 桌面项目，不支持这些安全性设置。
::: moniker-end

  在“发布”页面上设置了以下属性：

- `PublishUrl` 是应用程序将在 IDE 中发布到的位置。 如果未指定 `InstallUrl` 或 `UpdateUrl` 属性，则将其插入到 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序清单中。

- `ApplicationVersion` 指定 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序的版本。 这是一个四位数的版本号。 如果最后一位数字是“*”，则 `ApplicationRevision` 将替换为在生成时插入清单的值。

- `ApplicationRevision` 指定修订版本。 这是一个整数，每次在 IDE 中发布时都会递增。 请注意，对于在命令行上执行的生成，它不会自动递增。

- `Install` 确定应用程序是已安装的应用程序还是从 Web 运行的应用程序。

- `InstallUrl`（未显示）是用户安装应用程序的位置。 如果指定了此属性，则在启用了 `IsWebBootstrapper` 属性的情况下，会将该属性的值记录到 setup.exe 引导程序中。 如果未指定 `UpdateUrl`，它也会插入到应用程序清单中。

- `SupportUrl`（未显示）是已安装应用程序的“添加/删除程序”对话框中链接的位置。

  以下属性在“应用程序更新”对话框中设置，可从“发布”页面访问 。

- `UpdateEnabled` 指示应用程序是否应检查更新。

- `UpdateMode` 指定前台更新或后台更新。
::: moniker range=">=vs-2019"
   对于 .NET Core 3.1 或更高版本的项目，不支持后台。  
::: moniker-end
- `UpdateInterval` 指定应用程序检查更新的频率。
::: moniker range=">=vs-2019"
   对于 .NET Core 3.1 或更高版本，不支持此设置。
::: moniker-end

- `UpdateIntervalUnits` 指定 `UpdateInterval` 的值是以小时、天还是周为单位。
::: moniker range=">=vs-2019"
   对于 .NET Core 3.1 或更高版本，不支持此设置。
::: moniker-end

- `UpdateUrl`（未显示）是应用程序接收更新的位置。 如果指定了该属性，该属性的值将插入到应用程序清单中。

  以下属性在“发布选项”对话框中设置，可从“发布”页面访问 。

- `PublisherName` 指定安装或运行应用程序时系统显示的提示中所示的发布者名称。 对于已安装的应用程序，该属性还用于在“开始”菜单上指定文件夹名称。

- `ProductName` 指定在安装或运行应用程序时系统显示的提示中所示的产品名称。 对于已安装的应用程序，该属性还用于在“开始”菜单上指定快捷方式名称。

  以下属性在“先决条件”对话框中设置，可从“发布”页面访问 。

- `BootstrapperEnabled` 确定是否生成 setup.exe 引导程序。

- `IsWebBootstrapper` 确定 setup.exe 引导程序是通过 Web 还是在基于磁盘的模式下工作。

## <a name="installurl-supporturl-publishurl-and-updateurl"></a>InstallURL、SupportUrl、PublishURL 和 UpdateURL

 下表显示了用于 ClickOnce 部署的四个 URL 选项。

|URL 选项|说明|
|----------------|-----------------|
|`PublishURL`|如果要将 ClickOnce 应用程序发布到网站，则为必需。|
|`InstallURL`|可选。 如果安装站点与 `PublishURL` 不同，请设置此 URL 选项。 例如，可以将 `PublishURL` 设置为 FTP 路径并将 `InstallURL` 设置为 Web URL。|
|`SupportURL`|可选。 如果支持站点与 `PublishURL` 不同，请设置此 URL 选项。 例如，可以将 `SupportURL` 设置为公司的客户支持网站。|
|`UpdateURL`|可选。 如果更新位置与 `InstallURL` 不同，请设置此 URL 选项。 例如，可以将 `PublishURL` 设置为 FTP 路径并将 `UpdateURL` 设置为 Web URL。|

## <a name="see-also"></a>另请参阅

- <xref:Microsoft.Build.Tasks.GenerateBootstrapper>
- <xref:Microsoft.Build.Tasks.GenerateApplicationManifest>
- <xref:Microsoft.Build.Tasks.GenerateDeploymentManifest>
- [ClickOnce 安全性和部署](../deployment/clickonce-security-and-deployment.md)
- [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)
