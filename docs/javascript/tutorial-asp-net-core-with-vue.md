---
title: 使用 Vue 创建 ASP.NET Core 应用
description: 在本教程中，使用 ASP.NET Core 和 Vue 创建应用
ms.date: 11/08/2021
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
ms.openlocfilehash: 05c47320efe74f186786954bc608b445255f150a
ms.sourcegitcommit: 8b44ba7864f67afa476708d5092729345e689f93
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2021
ms.locfileid: "132861505"
---
# <a name="tutorial-create-an-aspnet-core-app-with-vue-in-visual-studio"></a>教程：在 Visual Studio 中使用 Vue 创建 ASP.NET Core 应用

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
- npm ([https://www.npmjs.com/](https://www.npmjs.com/)) 
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

1. 接下来，右键单击 Vue 项目并选择“属性”菜单，然后转到“调试”部分。  将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/asp-net-core-with-vue-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="set-the-startup-project"></a>设置启动项目

1. 右键单击解决方案并选择“设置启动项目”。 将启动项目从“单个启动项目”更改为“多个启动项目”。 为每个项目的操作选择“启动”。
  
1. 接下来，选择后端项目，将其移到前端之上，使它首先启动。

   :::image type="content" source="media/vs-2022/asp-net-core-with-vue-set-first-project.png" alt-text="选择第一个启动项目":::

## <a name="start-the-project"></a>启动项目

1. 启动项目之前，请确保端口号匹配。 转到 ASP.NET Core 项目中的 launchSettings.json 文件（在 Properties 文件夹中） 。 从 `applicationUrl` 属性获取端口号。

   如果有多个 `applicationUrl` 属性，请使用 `https` 终结点查找一个。 它看起来应该类似于 `https://localhost:7049`。

1. 然后，转到 Vue 项目的 vue.config.js 文件。 更新目标属性，以匹配 launchSettings.json 中的 `applicationUrl` 属性。

1. 若要启动项目，请按 F5 或选择窗口顶部的“开始”按钮 。 将显示两个命令提示符：

   - 正在运行的 ASP.NET Core API 项目
   - 运行 vue-cli-service serve 命令的 Vue CLI

应会显示一个 Vue 应用，该应用通过 API 填充。

## <a name="troubleshooting"></a>故障排除

你可能会看到以下错误：

```
[HPM] Error occurred while trying to proxy request /weatherforecast from localhost:4200 to https://localhost:5001 (ECONNREFUSED) (https://nodejs.org/api/errors.html#errors_common_system_errors)
```

如果看到此问题，很可能前端在后端之前启动。 看到后端命令提示符启动并运行后，只需在浏览器中刷新 Vue 应用即可。
