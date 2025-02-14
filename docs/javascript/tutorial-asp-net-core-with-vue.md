---
title: 使用 Vue 创建 ASP.NET Core 应用
description: 在本教程中，使用 ASP.NET Core 和 Vue 创建应用
ms.date: 03/15/2022
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
monikerRange: '>= vs-2022'
ms.openlocfilehash: b3ee695f4a1a12b3f2fc9ca4ba433e2949d50000
ms.sourcegitcommit: 2c4ca71e7711d9c4a468b1bcff026565c765952c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2022
ms.locfileid: "145172672"
---
# <a name="tutorial-create-an-aspnet-core-app-with-vue-in-visual-studio"></a>教程：在 Visual Studio 中使用 Vue 创建 ASP.NET Core 应用

 [!INCLUDE [Visual Studio](~/includes/applies-to-version/vs-windows-only.md)]

在本文中，你将了解如何生成 ASP.NET Core 项目来充当 API 后端，并生成 Vue 项目来充当 UI。

目前，Visual Studio 包含支持 Angular、React 和 Vue 的 ASP.NET Core 单页应用程序 (SPA) 模板。 这些模板在 ASP.NET Core 项目中提供内置的客户端应用文件夹，其中包含每个框架的基本文件和文件夹。

从 Visual Studio 2022 预览版 2 开始，可以使用本文中所述的方法创建具有以下功能的 ASP.NET Core 单页应用程序：

- 将客户端应用放在 ASP.NET Core 项目之外的独立项目中
- 基于计算机上安装的框架 CLI 创建客户端项目

> [!NOTE]
> 目前，必须手动发布前端项目（当前不支持发布工具）。 有关附加信息，请参阅 [https://github.com/MicrosoftDocs/visualstudio-docs/issues/7135](https://github.com/MicrosoftDocs/visualstudio-docs/issues/7135)。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- 安装了 Visual Studio 2022 预览版 2 或更高版本，以及 ASP.NET 和 Web 开发工作负载。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
  如果需要安装工作负载，但已安装 Visual Studio，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改” 。
- [https://www.npmjs.com/](https://www.npmjs.com/package/npm) npm () ，Node.js
- Vue CLI ([https://cli.vuejs.org/](https://cli.vuejs.org/))  

## <a name="create-the-frontend-app"></a>创建前端应用

1. 在“新建项目”对话框中，选择“创建新项目”。 

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的搜索栏中搜索 Vue，然后选择“独立 JavaScript Vue 模板”或“独立 TypeScript Vue 模板” 。

   :::image type="content" source="media/vs-2022/vue-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。 转到“其他信息”窗口时，请务必选中“为空的 ASP.NET Web API 项目添加集成”选项。  此选项将文件添加到 Vue 模板，以便稍后可以与 ASP.NET Core 项目挂钩。

   其他信息

创建项目后，你会看到一些新的和经修改的文件：

- aspnetcore-https.js
- vue.config.json（已修改）
- HelloWorld.vue（已修改）
- package.json（已修改）

## <a name="create-the-backend-app"></a>创建后端应用

1. 在解决方案资源管理器中，右键单击解决方案名称，将鼠标悬停在“添加”上，然后选择“新建项目”。  

   :::image type="content" source="media/vs-2022/asp-net-core-add-project.png" alt-text="添加新项目":::

1. 搜索并选择 ASP.NET Core Web API 项目。
 
   :::image type="content" source="media/vs-2022/asp-net-core-choose-web-api-template.png" alt-text="选择 Web API 模板":::

1. 为你的项目和解决方案命名。 转到“其他信息”窗口时，选择“.NET 6.0”作为目标框架。 

   创建项目后，解决方案资源管理器应如下所示：

   :::image type="content" source="media/vs-2022/asp-net-core-with-vue-solution-explorer.png" alt-text="查看解决方案资源管理器":::

1. 从 Properties 文件夹打开 `launchSettings.json`，然后在后端应用的 profiles 节下将默认端口更改为 5001 和 5003。

   ```json
   "profiles": {
     "yourbackendapp": {
       "commandName": "Project",
       "launchUrl": "swagger",
       "environmentVariables": {
         "ASPNETCORE_ENVIRONMENT": "Development"
       },
       "applicationUrl": "https://localhost:5001;http://localhost:5003",
       "dotnetRunMessages": true
     },
   ```

## <a name="set-the-project-properties"></a>设置项目属性

1. 在解决方案资源管理器中，右键单击 ASP.NET Core 项目，然后选择“属性”。

   :::image type="content" source="media/vs-2022/asp-net-core-project-properties.png" alt-text="打开项目属性"::: 
 
1. 转到“调试”菜单，然后选择“打开调试启动配置文件 UI”选项。 清除“启动浏览器”选项。

   :::image type="content" source="media/vs-2022/asp-net-core-with-vue-deselect-launch-browser.png" alt-text="打开调试启动配置文件 UI"::: 

   >[!NOTE]
   > 目前， *launch.json* 必须位于 *.vscode* 文件夹下。

## <a name="set-the-startup-project"></a>设置启动项目

1. 右键单击解决方案并选择“设置启动项目”。 将启动项目从“单个启动项目”更改为“多个启动项目”。 为每个项目的操作选择“启动”。
  
1. 接下来，选择后端项目，将其移到前端之上，使它首先启动。

   :::image type="content" source="media/vs-2022/asp-net-core-with-vue-set-first-project.png" alt-text="选择第一个启动项目":::

## <a name="start-the-project"></a>启动项目

1. 启动项目之前，请确保端口号匹配。 转到 ASP.NET Core 项目中的 launchSettings.json 文件（在 Properties 文件夹中） 。 从 `applicationUrl` 属性获取端口号。

   如果有多个 `applicationUrl` 属性，请使用 `https` 终结点查找一个。 它看起来应该类似于 `https://localhost:5001`。

1. 然后，转到 Vue 项目的 vue.config.js 文件。 更新目标属性，以匹配 launchSettings.json 中的 `applicationUrl` 属性。 更新时，该值应如下所示：

   ```js
   target: 'https://localhost:5001',
   ```

1. 若要启动项目，请按 F5 或选择窗口顶部的“开始”按钮 。 将显示两个命令提示符：

   - 正在运行的 ASP.NET Core API 项目
   - 运行 vue-cli-service serve 命令的 Vue CLI

   >[!NOTE]
   > 检查消息的控制台输出，例如指示更新Node.js版本的消息。

应会显示一个 Vue 应用，该应用通过 API 填充。

## <a name="troubleshooting"></a>故障排除

### <a name="proxy-error"></a>代理错误

你可能会看到以下错误：

```
[HPM] Error occurred while trying to proxy request /weatherforecast from localhost:4200 to https://localhost:5001 (ECONNREFUSED) (https://nodejs.org/api/errors.html#errors_common_system_errors)
```

如果看到此问题，很可能前端在后端之前启动。 看到后端命令提示符启动并运行后，只需在浏览器中刷新 Vue 应用即可。

否则，如果端口正在使用，请尝试 *launchSettings.json* 中的 5002 并 *vue.config.js*。

### <a name="outdated-version-of-vue"></a>过时版本的 Vue

如果在创建项目时看到控制台消息 **找不到文件“C：\Users\Me\source\repos\vueprojectname\package.json”** ，则可能需要更新 Vue CLI 的版本。 更新 Vue CLI 后，可能还需要在 *C：\Users\\[yourprofilename\]*] 中删除 *.vuerc* 文件。

### <a name="docker"></a>Docker

如果在创建 Web API 项目时启用 Docker 支持，则后端可能会开始使用 Docker 配置文件，而不侦听配置的端口 5001。 若要解决问题，请执行以下操作：

通过添加以下属性编辑 launchSettings.json 中的 Docker 配置文件：

```json
"httpPort": 5003, 
"sslPort": 5001  
```

或者，使用以下方法重置：

1. 在解决方案属性中，将后端应用设置为启动项目。
1. 在“调试”菜单中，使用 **“"开始"菜单**”按钮下拉菜单将配置文件切换到后端应用的配置文件。
1. 接下来，在解决方案属性中，重置为多个启动项目。
