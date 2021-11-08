---
title: 通过导入发布设置来发布到 IIS
description: 创建并导入发布配置文件，以便将应用程序从 Visual Studio 部署到 IIS
ms.date: 10/22/2021
ms.topic: tutorial
helpviewer_keywords:
- deployment, publish settings
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-deployment
ms.workload:
- multiple
ms.openlocfilehash: baa81fc1eb735a790d6040643fa096be64858c18
ms.sourcegitcommit: 7a820b7698a8dcf076eb36e3d766fb0751f56bb1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2021
ms.locfileid: "131127762"
---
# <a name="get-publish-settings-from-iis-and-import-into-visual-studio"></a>从 IIS 中获取发布设置并将其导入 Visual Studio

可使用“发布”工具导入发布设置，然后部署应用。 本文使用 IIS 的发布设置。

这些步骤适用于 ASP.NET 和 ASP.NET Core Web 应用程序。

> [!NOTE]
> 发布设置文件 (\*.publishsettings) 与发布配置文件 (\*.pubxml) 不同 。 发布设置文件是在 IIS 中创建的，然后可以将其导入 Visual Studio。 Visual Studio 创建发布配置文件。

## <a name="prerequisites"></a>先决条件

* [Visual Studio](https://www.visualstudio.com/downloads) 随 ASP.NET 和 Web 开发工作负载一起安装。 如果已安装 Visual Studio：

  * 通过选择“帮助” > “检查更新”，在 Visual Studio 中安装最新更新。
  * 通过选择“工具” > “获取工具和功能”，添加工作负荷。

* 服务器上必须运行 Windows Server 2012、Windows Server 2016 或 Windows Server 2019，并且必须正确安装 [IIS Web 服务器角色](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45#solution)（需要生成发布设置文件 (\*.publishsettings)）。 该服务器上还必须安装 ASP.NET 4.5 或 ASP.NET Core。

  * 若要安装 ASP.NET Core，请参阅 [使用 IIS 在 Windows 上托管 ASP.NET Core](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration)。 对于 ASP.NET Core，请确保将“应用程序池”配置为使用“无托管代码”，如文章中所述。

  * 若要安装 ASP.NET 4.5，请参阅[使用 ASP.NET 3.5 和 ASP.NET 4.5 的 IIS 8.0](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45)。

  > [!NOTE]
  > Windows 上的 IIS 不支持生成发布设置。 不过，你仍可以使用 Visual Studio 中的“发布”工具发布到 IIS。

## <a name="install-and-configure-web-deploy-on-windows-server"></a>在 Windows Server 上安装和配置 Web 部署

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

## <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>在 Windows Server 上的 IIS 中创建发布设置文件

[!INCLUDE [create-publish-settings-iis](../deployment/includes/create-publish-settings-iis.md)]

## <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>在 Visual Studio 中导入发布设置并进行部署

[!INCLUDE [import-publish-settings](../deployment/includes/import-publish-settings-vs.md)]

应用成功部署后，它应自动启动。

## <a name="common-issues"></a>常见问题

首先，在 Visual Studio 的“输出”窗口中查看状态信息，并查看你的错误消息。 此外：

- 如果无法使用主机名连接到主机，请尝试改用 IP 地址。
- 确保远程服务器上已打开所需的端口。
- 对于 ASP.NET Core，需要确保在 IIS 中将 DefaultAppPool 的应用程序池字段设置为“无托管代码” 。
- 验证应用中使用的 ASP.NET 版本是否与服务器上安装的版本相同。 对于你的应用，你可在“属性”页面上查看和设置版本。 若要将应用设置为其他版本，必须安装该版本。
- 如果应用尝试打开，但显示证书警告，请选择信任站点。 如果你已关闭警告，则可在项目中编辑 *.pubxml 文件，并添加以下元素：`<AllowUntrustedCertificate>true</AllowUntrustedCertificate>`。 此设置仅用于测试！
- 如果在 Visual Studio 中无法启动应用，请在 IIS 中启动应用来测试它是否正确部署。