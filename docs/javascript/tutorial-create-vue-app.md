---
title: 创建 Vue.js 应用程序
description: 本教程介绍如何在 Visual Studio 中创建简单的 Vue.js 应用程序。
ms.date: 07/30/2021
ms.custom: vs-acquisition
ms.topic: tutorial
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
dev_langs:
- JavaScript
ms.workload:
- nodejs
monikerRange: '>= vs-2022'
ms.openlocfilehash: 33e69c5e828120ab9449296c957ed7c00f71d7e1
ms.sourcegitcommit: 2430a38f23ac17b65dd8d3baa806e90433aba24f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/04/2021
ms.locfileid: "115094900"
---
# <a name="create-a-vuejs-app"></a>创建 Vue.js 应用程序

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，你可以创建并运行简单的 Vue.js 前端 Web 应用程序。

## <a name="prerequisites"></a>先决条件

确保已安装以下各项：

- npm ([https://www.npmjs.com/](https://www.npmjs.com/)) 
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

按 F5 或选择窗口顶部的“开始”按钮。  此时会出现命令提示符：

- npm 运行 vue-cli-service start 命令

接下来，你会看到基本 Vue.js 应用！