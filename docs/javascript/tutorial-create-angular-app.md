---
title: 创建 Angular 应用
description: 本教程介绍如何在 Visual Studio 中创建简单的 Angular 应用程序。
ms.date: 07/30/2021
ms.custom: vs-acquisition
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
ms.openlocfilehash: f71cfd879519d1f96ee4f5ec2ca852c2812d65f8
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139549293"
---
# <a name="create-an-angular-app"></a>创建 Angular 应用

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你可以创建并运行简单的 Angular 前端 Web 应用程序。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- Visual Studio 2022 预览版 2 或更高版本。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
- npm ([https://www.npmjs.com/](https://www.npmjs.com/package/npm)) ，包含在 Node.js
- AngularCLI ([https://angular.io/cli](https://angular.io/cli)) 这可以是你选择的版本

## <a name="create-your-app"></a>创建应用

1. 在“新建项目”对话框中，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的Angular搜索栏中搜索"模板"，然后选择"独立 **TypeScript Angular模板"**。

   :::image type="content" source="media/vs-2022/angular-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。

   当进入"其他信息"窗口时，请务必不要选中"为空值添加集成 **ASP.NET Web API Project** 选项。 如果添加了 ASP.NET Core 项目，此选项将文件添加到 Angular 模板，以便稍后可以与 ASP.NET Core 项目挂钩。

   其他信息

## <a name="set-the-project-properties"></a>设置项目属性

1. 在解决方案资源管理器中，右键单击 Angular 项目，选择“属性”，然后转到“调试”部分 。

1. 将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/angular-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="build-your-project"></a>生成项目

选择“生成” > “生成解决方案”以生成项目 。

请注意，初始生成可能需要一段时间，因为 Angular CLI 将运行 npm install 命令。

## <a name="start-your-project"></a>启动项目

按 **F5** **或选择窗口** 顶部的"开始"按钮，你将看到命令提示符：

- 运行 ng start 的 Angular CLI

   >[!NOTE]
   > 检查控制台输出中的消息，例如指示更新版本的消息Node.js。

接下来，应会看到基本Angular应用显示！

## <a name="next-steps"></a>后续步骤

对于 ASP.NET Core集成：

> [!div class="nextstepaction"]
> [使用 Angular 创建 ASP.NET Core 应用](tutorial-asp-net-core-with-angular.md)
