---
title: 扩展的解析
description: 介绍 Visual Studio 扩展的结构
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 57a12f428211f4799fa610bf729110743de34f76
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515936"
---
# <a name="anatomy-of-a-visual-studio-extension"></a>Visual Studio 扩展的剖析

vsix 包是一个 .vsix 文件，其中包含一个或多个 Visual Studio 扩展，以及 Visual Studio 用于分类和安装扩展的元数据。 VSIX 包格式遵循 (OPC) 标准的开放打包约定，这意味着可以打开 ZIP 文件的任何工具都可以打开它。

扩展项目是一个 c # 项目，其中包含几个使其唯一的附加方案。 以下视频将探讨扩展项目，以更好地了解扩展项目的工作方式：

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPhtJ]

## <a name="file-structure"></a>文件结构
使用 **VSIX Project w/Command (Community)** 模板创建新扩展时，文件结构如下所示：

:::image type="content" source="../media/new-project-files.png" alt-text="VSIX 项目的文件结构。":::

**Source.extension.vsixmanifest** 文件是主文件。 它是一个 XML 文件，其中包含 Visual Studio 所使用的扩展的相关信息。 扩展的所有组件都在 **source.extension.vsixmanifest** 文件中注册。 它是 VSIX 项目中唯一必需的文件。

**VSCommandTable. .vsct** 文件是声明命令的位置。 它是一个 XML 文件，包含按钮命令、菜单、键盘快捷键绑定等的定义。 文件将其内容编译到输出 .dll 中的 blob，Visual Studio 使用该 blob 构造其整个命令表菜单结构。 此文件仅声明命令表中的组件;它不处理任何命令调用。

**\* Package .cs** 文件是包类，包类是大多数扩展的入口点。 在这里，你经常会发现命令处理程序、工具窗口、选项页、服务以及其他已注册组件。

## <a name="compilation"></a>编译
该项目将编译为位于 */bin/debug* 或 */bin/release* 文件夹中的 .vsix 文件，这取决于当前的解决方案生成配置。 *Visual Studio 扩展开发*[工作负荷](get-tools.md)提供专用的 MSBuild 目标和任务来处理 VSIX 项目风格。

当 VSIX 项目生成时，它会自动将自身部署到实验实例。 可在 VSIX 项目设置中对此进行控制： 

:::image type="content" source="../media/deploy-vsix-experimental-instance.png" alt-text="VSIX 项目属性。":::

## <a name="experimental-instance"></a>实验实例
为了保护您的 Visual Studio 开发环境，使其不受未经测试的应用程序的可能更改，VS SDK 提供了可用于试验的实验空间。 您可以像平常一样使用 Visual Studio 开发新应用程序，但使用此实验实例运行这些应用程序。

具有 VSIX 包的每个应用程序在调试模式下启动 Visual Studio 的实验实例。

如果要启动特定解决方案外 Visual Studio 的实验实例，请在命令窗口中运行以下命令：

```shell
devenv.exe /RootSuffix Exp
```

有关更多扩展性概念，请查看 [有用的资源](useful-resources.md)，这些资源将为遵循此工具包提供便利。
