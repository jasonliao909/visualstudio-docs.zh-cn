---
title: 启动 Docker Compose 服务的子集
description: 了解如何使用 Docker Compose 启动配置文件，以及如何控制在 Visual Studio 中使用 Docker Compose 时要启动的服务。
author: ghogen
manager: jmartens
ms.technology: vs-container-tools
ms.devlang: dotnet
ms.topic: how-to
ms.date: 05/10/2021
ms.author: ghogen
monikerRange: '>=vs-2019'
ms.openlocfilehash: d91e58a554847fa5a713b120d2896c2e8120b2a8
ms.sourcegitcommit: ff81d69902e869b227d9ceb6e95023d1c63425b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2021
ms.locfileid: "129595139"
---
# <a name="launch-a-subset-of-compose-services"></a>启动 Compose 服务的子集

如果应用程序包含多个服务并且使用的是 Docker Compose，可以通过在 Docker Compose 启动设置中创建或编辑现有启动配置文件来配置要运行和调试的服务。 启动配置文件允许仅动态运行对当前场景重要的服务。 可以创建启动配置文件并从中进行选择，以自定义调试体验并设置特定的启动操作，例如 `Browser Launch URL`。 你还可以选择单独选择每个服务或选择 Docker Compose 配置文件，这还将查看 Compose 文件以确定要运行的服务组。

有关 Docker Compose 配置文件的信息，请参阅[使用 Compose 配置文件](https://docs.docker.com/compose/profiles/)。
 
## <a name="prerequisites"></a>先决条件

- [Visual Studio 2019 版本 16.10](https://visualstudio.microsoft.com/vs/) 或更高版本
- [使用 Docker Compose 进行容器编排](tutorial-multicontainer.md)的 .NET 解决方案

## <a name="manage-launch-settings"></a>管理启动设置

考虑以下 Docker Compose 项目，其中 docker-compose.yml 文件具有五个服务和三个 Compose 配置文件（web、web1 和 web2）。

```yml
version: '3.9'

services:
  webapplication1:
    image: ${DOCKER_REGISTRY-}webapplication1
    profiles: [web, web1]
    build:
      context: .
      dockerfile: WebApplication1/Dockerfile

  webapplication2:
    image: ${DOCKER_REGISTRY-}webapplication2
    profiles: [web, web2]
    build:
      context: .
      dockerfile: WebApplication2/Dockerfile

  webapplication3:
    image: ${DOCKER_REGISTRY-}webapplication3
    profiles: [web]
    build:
      context: .
      dockerfile: WebApplication3/Dockerfile

  external1:
    image: redis

  external2:
    image: redis

```

可以通过几个选项打开“Docker Compose 启动设置”对话框：
- 在 Visual Studio 中，选择“调试” > “管理 Docker Compose 启动设置” ：

    ![调试“管理 Compose 设置”菜单项的屏幕截图](media/launch-settings/debug-dropdown-manage-compose.png)

- 右键单击 Visual Studio `docker-compose` 项目并选择“管理 Docker Compose 启动设置”

    ![上下文菜单项的屏幕截图](media/launch-settings/launch-settings-context-menu.png)

- 使用“快速启动”(Ctrl+Q) 并搜索“Docker Compose”找到上述命令  。

在下面的示例中，`web1` Compose 配置文件处于选中状态，这将对“服务”列表进行筛选，使该配置文件中仅包含五个服务中的三个服务：

![“启动设置对话框的屏幕截图”](media/launch-settings/launch-settings-create-profile.png)

>[!NOTE]
> Docker Compose 配置文件部分仅在 docker-compose.yml 文件中定义了配置文件时才会出现。

下一个示例演示在单个服务之间进行选择，而不是筛选 Compose 配置文件中的服务。 在这里，我们展示创建名为 `test2` 的新启动配置文件后对话框的外观，该配置文件仅启动五个服务中的两个，即包含调试的 `webapplication1` 和不包含调试的 `webapplication2`。  此启动配置文件还会在应用程序启动时启动浏览器并在其中打开 `webapplication1` 的主页。 

![取消选择了某些服务的启动设置对话框的屏幕截图](media/launch-settings/launch-settings-selected.png)

此信息将保存在 launchSettings.json 中，如下所示

```json
{
    "profiles": {
      "test2": {
        "commandName": "DockerCompose",
        "composeLaunchServiceName": "webapplication1",
        "serviceActions": {
          "external1": "DoNotStart",
          "external2": "DoNotStart",
          "webapplication1": "StartDebugging",
          "webapplication2": "StartWithoutDebugging",
          "webapplication3": "DoNotStart"
        },
        "composeLaunchAction": "LaunchBrowser",
        "commandVersion": "1.0",
        "composeLaunchUrl": "{Scheme}://localhost:{ServicePort}"
      }
   }
}
```

## <a name="create-a-launch-profile-that-uses-a-docker-compose-profile"></a>创建使用 Docker Compose 配置文件的启动配置文件

还可以通过创建使用 Compose 配置文件的 Visual Studio 启动配置文件来进一步自定义启动行为。

要创建其他使用 Compose 配置文件的配置文件，请选择“使用 Docker Compose 配置文件”并选择 `web1`。 现在启动配置文件包括三个服务 - `webapplication1`（属于 `web` 和 `web1` Compose 配置文件）、`external1` 和 `external2`。 默认情况下，不包含源代码的服务（例如 `external1` 和 `external2`）都具有“启动(不调试)”的默认操作。 包含源代码的 .NET 应用程序将默认为“启动调试”。

> [!IMPORTANT]
> 如果服务未指定 Compose 配置文件，它将隐式包含在所有 Compose 配置文件中。

![创建了其他配置文件的启动设置对话框的屏幕截图](media/launch-settings/launch-settings-create-profile.png)

此信息将被保存，如以下代码所示。 除非更改默认操作，否则不会保存服务的配置及其默认操作。

```json
{
  "profiles": {
    "test1": {
      "commandName": "DockerCompose",
      "composeProfile": {
         "includes": [
            "web1"
         ]
      },
      "commandVersion": "1.0"
    }
  }
}
```

此外，还可以将 webapplication1 的操作更改为“启动(不调试)”。 然后，launchSettings.json 中的设置会如以下代码所示：

```json
{
  "profiles": {
    "test1": {
        "commandName": "DockerCompose",
        "composeProfile": {
          "includes": [
              "web1"
              ],
          "serviceActions": {
              "webapplication1": "StartWithoutDebugging"
          }
        },
    "commandVersion": "1.0"
    }
  }
}
```

## <a name="properties"></a>属性

以下是 launchSettings.json 中每个属性的说明：

|属性| 说明|
| - | - |
|commandName| 命令的名称。 默认为“DockerCompose”|
|commandVersion| 用于管理 DockerCompose 启动配置文件架构的版本号。|
|composeProfile| 定义启动配置文件定义的父属性。 它的子属性是 `includes` 和 `serviceActions`|
|composeProfile - includes | 构成启动配置文件的 Compose 配置文件名称列表。|
|composeProfile - serviceActions | 列出选定的 Compose 配置文件、服务以及每个服务的启动操作|
|serviceActions | 列出选定的服务和启动操作。|
|composeLaunchAction| 指定要针对 F5 或 Ctrl+F5 执行的启动操作  。 允许的值为 None、LaunchBrowser 和 LaunchWCFTestClient。|
|composeLaunchUrl| 启动浏览器时将使用的 URL。 有效的替换令牌为“{ServiceIPAddress}”、“{ServicePort}”和“{Scheme}”。 例如：{Scheme}://{ServiceIPAddress}:{ServicePort}|
|composeLaunchServiceName| 指定用于替换 composeLaunchUrl 中的令牌的服务。|

## <a name="next-steps"></a>后续步骤

阅读 [Visual Studio 容器工具和调试概述](container-build.md)，详细了解容器工具的工作原理。

## <a name="see-also"></a>另请参阅

- [Visual Studio 容器工具启动设置](container-launch-settings.md)

- [Docker Compose 生成设置](docker-compose-properties.md)
