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
ms.openlocfilehash: 1b40a03c63665be09ecea5c28fb8e82dcc69c7a7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126641564"
---
# <a name="create-an-angular-app"></a>创建 Angular 应用

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你可以创建并运行简单的 Angular 前端 Web 应用程序。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- Visual Studio 2022 预览版 2 或更高版本。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
- npm ([https://www.npmjs.com/](https://www.npmjs.com/)) 
- AngularCLI ([https://angular.io/cli](https://angular.io/cli)) 这可以是你选择的版本

## <a name="create-your-app"></a>创建应用

1. 在“新建项目”对话框中，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的搜索栏中搜索“Angular”，然后选择“独立 Angular 模板”。

   :::image type="content" source="media/vs-2022/angular-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。 

   转到“其他信息”窗口时，请务必不要选中“为空的 ASP.NET Web API 项目添加集成”选项。 如果添加了 ASP.NET Core 项目，此选项将文件添加到 Angular 模板，以便稍后可以与 ASP.NET Core 项目挂钩。

   其他信息

## <a name="set-the-project-properties"></a>设置项目属性

1. 在解决方案资源管理器中，右键单击 Angular 项目，选择“属性”，然后转到“调试”部分 。

1. 将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/angular-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="build-your-project"></a>生成项目

选择“生成” > “生成解决方案”以生成项目 。

请注意，初始生成可能需要一段时间，因为 Angular CLI 将运行 npm install 命令。

## <a name="start-your-project"></a>启动项目

按 F5 或选择窗口顶部的“开始”按钮。  此时会出现命令提示符：

- 运行 ng start 的 Angular CLI

接下来，你会看到基本 Angular 应用！