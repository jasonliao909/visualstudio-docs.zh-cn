---
title: launchSettings.json 支持
description: 本文档介绍了 Visual Studio for Mac 中对 launchSettings.json 的支持
author: jmatthiesen
ms.author: jomatthi
manager: dominicn
ms.date: 05/02/2022
ms.custom: devdivchpfy22
ms.assetid: a556f9d7-86a8-408e-aa54-392584845889
ms.openlocfilehash: 657076b7f49f976e0fd42439ab6c99f20ab5ddff
ms.sourcegitcommit: 3034382894e610b55f3ad07e737fa59b91680869
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2022
ms.locfileid: "144548551"
---
# <a name="launchsettingsjson"></a>launchSettings.json

[!INCLUDE [Visual Studio for Mac](~/includes/applies-to-version/vs-mac-only.md)]

开发 ASP.NET Core 项目时，可以通过自定义 launchSettings.json 文件的内容来配置在开发场景中启动项目的方式。 在 Visual Studio for Mac 中，可以通过使用“项目选项”UI 或直接编辑来更新此文件。 此配置文件同样可在 Windows 上运行 Visual Studio 时使用，或在使用 `dotnet` 的命令行中使用。 此文件存储在 Properties 文件夹下的项目中。

有关更多详细信息，请参阅[在 ASP.NET Core 中使用多种环境](/aspnet/core/fundamentals/environments)。 本文将介绍在 Visual Studio for Mac 中更新此文件的方法。

## <a name="update-the-start-configuration-by-using-visual-studio-for-mac"></a>使用 Visual Studio for Mac 更新启动配置

可以直接在 Visual Studio for Mac 中编辑 _launchSettings.json_ 文件，也可以使用项目选项对其进行编辑。 若要转到项目选项，请右键单击项目，然后选择“选项”。

![Project快捷菜单，其中选择了“选项”，以使用 Visual Studio for Mac 更新开始配置。](media/vsmac-ctx-proj-options.png)

选择“运行” > “配置” > “默认”。

![项目选项中的“运行”、“配置”和“默认”，以使用Visual Studio for Mac更新启动配置。](media/vsmac-run-config-default.png)

主要是，在此处配置两项内容：

- 环境变量
- 项目的应用 URL

## <a name="configure-environment-variables"></a>配置环境变量

可以使用网格指定环境变量的值。 在 Visual Studio for Mac 中启动应用程序时，将设置这些环境变量。 开发 ASP.NET Core 应用程序时，应注意特殊的环境变量 `ASPNETCORE_ENVIRONMENT`。 若要了解详细信息，请参阅[在 ASP.NET Core 中使用多个环境](/aspnet/core/fundamentals/environments)。

## <a name="configure-the-start-url"></a>配置启动 URL

要配置用于启动应用程序的 URL，请转到“ASP.NET Core”选项卡。

![项目选项中的应用程序 URL，用于配置应用程序将启动的 URL。](media/vsmac-run-config-default-aspnetcore.png)

可以在此指定启动应用程序时，应用程序将侦听的 URL。
