---
title: 使用 Node.js REPL
description: Visual Studio 支持与 Node.js 运行时进行交互
ms.date: 12/04/2018
ms.topic: how-to
ms.devlang: javascript
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-javascript
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 8dc3cbe7fef2c5940a8e87c2f085e52cdd7b2659
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122048136"
---
# <a name="work-with-the-nodejs-interactive-window"></a>使用 Node.js 交互式窗口

Visual Studio 的 Node.js 工具包括一个用于已安装的 Node.js 运行时的交互窗口。 可在此窗口中输入 JavaScript 代码并立即查看结果，还可执行 npm 命令，与当前项目进行交互。 交互窗口是称为 REPL (**R** ead/**E** valuate/**P** rint **L** oop)。

## <a name="open-the-interactive-window"></a>打开交互窗口

可以通过右键单击解决方案资源管理器中的 Node.js 项目节点并选择“打开 Node.js 交互式窗口”来打开交互式窗口。

![项目上下文菜单中的 Node.js 交互式窗口](../javascript/media/interactivewindow-open-from-project.png)

用于打开 Node.js 交互式窗口的默认快捷键为 [CTRL] + K、N。或者，可以通过选择“视图” > “窗口” > “Node.js 交互式窗口”，从工具栏中打开窗口。

## <a name="use-the-repl"></a>使用 REPL

打开后，可以输入命令。

![Node.js 交互式窗口](../javascript/media/interactivewindow.png)

交互式窗口有多个内置命令，这些命令以点为前缀和开头，便于与声明的 JavaScript 函数相区别。 支持以下命令：

“.cls”、“.clear”清除编辑器窗口的内容，使历史记录和执行上下文保持不变。

“.help”显示有关指定命令的帮助，如果未指定，则显示所有可用命令和键绑定的相关帮助信息。

“.info”显示有关当前使用的 Node.js 可执行文件的信息。

“.npm”运行 npm 命令。 如果解决方案包含多个项目，使用 `.npm [projectname] <npm arguments>` 指定目标项目。

“.reset”将执行环境重置为初始状态，保留历史记录。

“.save”将当前 REPL 会话保存到文件中。