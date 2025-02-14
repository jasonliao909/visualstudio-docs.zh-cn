---
title: 创建 React 应用
description: 本教程介绍如何在 Visual Studio 中创建简单的 React 应用程序。
ms.date: 01/28/2022
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
ms.openlocfilehash: b5ed1575427bbb89cd09e61b2156ab7ba69d463f
ms.sourcegitcommit: edf8137cd90c67b6078a02c93094f7e1c3bf8930
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "139549186"
---
# <a name="create-a-react-app"></a>创建 React 应用

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你可以创建并运行简单的 React 前端 Web 应用程序。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- Visual Studio 2022 或更高版本。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
- npm ([https://www.npmjs.com/](https://www.npmjs.com/package/npm)) ，随附 Node.js
- npx ([https://www.npmjs.com/package/npx](https://www.npmjs.com/package/npx))

## <a name="create-your-app"></a>创建应用

1. 在“新建项目”对话框中，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的搜索栏中搜索 React，然后根据偏好选择“独立 JavaScript React 模板”或“独立 TypeScript React 模板” 。

   :::image type="content" source="media/vs-2022/react-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。 

   如果之前选择了“独立 JavaScript React 模板”，转到“其他信息”窗口时，请不要选中“为空的 ASP.NET Web API 项目添加集成”选项。 如果添加了 ASP.NET Core 项目，此选项将文件添加到 React 模板，以便稍后可以与 ASP.NET Core 项目挂钩。

   其他信息

   请注意，创建 React 项目需要一些时间，因为此时运行的 create-react-app 命令也运行 npm install 命令

## <a name="set-the-project-properties"></a>设置项目属性

1. 在解决方案资源管理器中，右键单击 React 项目，选择“属性”，然后转到“调试”部分 。

1. 将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/react-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="build-your-project"></a>生成项目

选择“生成” > “生成解决方案”以生成项目 。

## <a name="start-your-project"></a>启动项目

按 **F5** 或选择窗口顶部的 " **启动** " 按钮，此时将显示命令提示符：

- 运行 react-scripts start 命令的 npm

>[!NOTE]
> 检查控制台输出中的消息，如消息，指导您更新 Node.js 的版本。

接下来，你会看到基本 React 应用！

## <a name="next-steps"></a>后续步骤

对于 ASP.NET Core 集成：

> [!div class="nextstepaction"]
> [使用 React 创建 ASP.NET Core 应用](tutorial-asp-net-core-with-react.md)