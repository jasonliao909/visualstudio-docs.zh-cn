---
title: 使用 React 创建 ASP.NET Core 应用
description: 在本教程中，使用 ASP.NET Core 和 React 创建应用
ms.date: 07/19/2021
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
ms.openlocfilehash: 4d6fefdda40e550a62616a82734a84037c0c10b0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126644399"
---
# <a name="tutorial-create-an-aspnet-core-app-with-react-in-visual-studio"></a>教程：在 Visual Studio 中使用 React 创建 ASP.NET Core 应用

在本文中，你将了解如何生成 ASP.NET Core 项目来充当 API 后端，并生成 React 项目来充当 UI。

目前，Visual Studio 包含支持 Angular 和 React 的 ASP.NET Core 单页应用程序 (SPA) 模板。 这些模板在 ASP.NET Core 项目中提供内置的客户端应用文件夹，其中包含每个框架的基本文件和文件夹。

从 Visual Studio 2022 预览版 2 开始，可以使用本文中所述的方法创建具有以下功能的 ASP.NET Core 单页应用程序：

- 将客户端应用放在 ASP.NET Core 项目之外的独立项目中
- 基于计算机上安装的框架 CLI 创建客户端项目

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- 安装了 Visual Studio 2022 预览版 2 或更高版本，以及 ASP.NET 和 Web 开发工作负载。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
  如果需要安装工作负载，但已安装 Visual Studio，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改” 。
- npm ([https://www.npmjs.com/](https://www.npmjs.com/)) 
- npx ([https://www.npmjs.com/package/npx](https://www.npmjs.com/package/npx))

## <a name="create-the-frontend-app"></a>创建前端应用

1. 在“新建项目”对话框中，选择“创建新项目”。 

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的搜索栏中搜索“React”，然后选择“独立 JavaScript React 模板”。 （本教程当前不支持独立 TypeScript React模板。）

   :::image type="content" source="media/vs-2022/react-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。 转到“其他信息”窗口时，请务必选中“为空的 ASP.NET Web API 项目添加集成”选项。  此选项将文件添加到 React 模板，以便稍后可以与项目 ASP.NET Core 挂钩。

   其他信息

   创建项目后，你会看到一些新的和经修改的文件：

   - aspnetcore-https.js
   - aspnetcore-react.js
   - setupProxy.js
   - App.js (modified)
   - App.test.js (modified)

## <a name="create-the-backend-app"></a>创建后端应用

1. 在解决方案资源管理器中，右键单击解决方案名称，将鼠标悬停在“添加”上，然后选择“新建项目”。  

   :::image type="content" source="media/vs-2022/asp-net-core-add-project.png" alt-text="添加新项目":::

1. 搜索并选择 ASP.NET Core Web API 项目。
 
   :::image type="content" source="media/vs-2022/asp-net-core-choose-web-api-template.png" alt-text="选择 Web API 模板":::

1. 为你的项目和解决方案命名。 转到“其他信息”窗口时，选择“.NET 6.0”作为目标框架。 

   创建项目后，解决方案资源管理器应如下所示：

   :::image type="content" source="media/vs-2022/asp-net-core-with-react-solution-explorer.png" alt-text="查看解决方案资源管理器":::

## <a name="set-the-project-properties"></a>设置项目属性

1. 右键单击 ASP.NET Core 项目并选择“属性”。

   :::image type="content" source="media/vs-2022/asp-net-core-project-properties.png" alt-text="打开项目属性"::: 
 
1. 转到“调试”菜单，然后选择“打开调试启动配置文件 UI”选项。 取消选中“启动浏览器”选项。

   :::image type="content" source="media/vs-2022/asp-net-core-with-react-deselect-launch-browser.png" alt-text="打开调试启动配置文件 UI"::: 

1. 接下来，右键单击 React 项目并选择“属性”菜单，然后转到“调试”部分。  将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/asp-net-core-with-react-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="set-the-startup-project"></a>设置启动项目

1. 右键单击解决方案并选择“设置启动项目”。 将启动项目从“单个启动项目”更改为“多个启动项目”。 为每个项目的操作选择“启动”。
  
1. 接下来，选择后端项目，将其移到前端之上，使它首先启动。

   :::image type="content" source="media/vs-2022/asp-net-core-with-react-startup-project.png" alt-text="选择启动项目":::

## <a name="start-the-project"></a>启动项目

按 F5 或选择窗口顶部的“开始”按钮。  将显示两个命令提示符：

- 正在运行的 ASP.NET Core API 项目
- 运行 react-scripts start 命令的 npm

应会显示一个 React 应用，该应用通过 API 填充。

## <a name="troubleshooting"></a>故障排除

你可能会看到以下错误：

```
[HPM] Error occurred while trying to proxy request /weatherforecast from localhost:4200 to https://localhost:5001 (ECONNREFUSED) (https://nodejs.org/api/errors.html#errors_common_system_errors)
```

如果看到此问题，很可能前端在后端之前启动。 看到后端命令提示符启动并运行后，只需在浏览器中刷新 React 应用即可。
