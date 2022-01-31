---
title: 创建 Vue.js 应用程序
description: 本教程介绍如何在 Visual Studio 中创建简单的 Vue.js 应用程序。
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
ms.openlocfilehash: 3dc5470906bf189e11d9252b4a4177ffe485dba8
ms.sourcegitcommit: 20f9529648e69707063dccb2b15089bf4e9bf639
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2022
ms.locfileid: "137886640"
---
# <a name="create-a-vuejs-app"></a>创建 Vue.js 应用程序

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你可以创建并运行简单的 Vue.js 前端 Web 应用程序。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- Visual Studio 2022 预览版 2 或更高版本。 请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/)页，进行免费安装。
- npm ([https://www.npmjs.com/](https://www.npmjs.com/package/npm)) ，随附 Node.js
- Vue.js ([Installation | Vue.js (vuejs.org)](https://v3.vuejs.org/guide/installation.html#npm))
- Vue.js CLI ([(Installation | Vue.js (vuejs.org)](https://v3.vuejs.org/guide/installation.html#cli))

## <a name="create-your-app"></a>创建应用

1. 在“新建项目”对话框中，选择“创建新项目”。

   :::image type="content" source="media/vs-2022/create-new-project.png" alt-text="创建新项目":::

1. 在顶部的搜索栏中搜索 Vue，然后根据偏好选择“独立 JavaScript Vue 模板”或“独立 TypeScript Vue 模板” 。

   :::image type="content" source="media/vs-2022/vue-choose-template.png" alt-text="选择模板":::

1. 为你的项目和解决方案命名。 

## <a name="set-the-project-properties"></a>设置项目属性

1. 在解决方案资源管理器中，右键单击 Vue.js 项目，选择“属性”，然后转到“调试”部分 。

1. 将“调试器”更改为“launch.json”选项。
 
   :::image type="content" source="media/vs-2022/vue-choose-debugger.png" alt-text="选择调试器 (launch.json)":::

## <a name="build-your-project"></a>生成项目

选择“生成” > “生成解决方案”以生成项目 。

## <a name="start-your-project"></a>启动项目

按 **F5** 或选择窗口顶部的 " **启动** " 按钮，此时将显示命令提示符：

- npm 运行 vue-cli-service start 命令

   >[!NOTE]
   > 检查控制台输出中的消息，如消息，指导您更新 Node.js 的版本。

接下来，你会看到基本 Vue.js 应用！