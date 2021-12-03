---
title: 获取工具
description: 需要编写扩展Visual Studio及其安装方法的列表。
ms.date: 12/01/2021
ms.topic: conceptual
author: madskristensen
ms.author: madsk
manager: pchapman
ms.prod: visual-studio-windows
ms.technology: vs-ide-sdk
ms.custom: cookbook
ms.openlocfilehash: 51a05667664de6bfc30d910974c70139709e96a3
ms.sourcegitcommit: a149b3a034bb555ad217656c0ec8bc1672b1e215
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2021
ms.locfileid: "133515830"
---
# <a name="get-the-tools-needed-to-write-visual-studio-extensions"></a>获取编写扩展Visual Studio工具

若要编写扩展，必须安装扩展性工作负载。 从技术上来说，这一组文档使用名为 *Extensibility Essentials* 的社区驱动扩展。 每个版本的 Visual Studio都有其自己的版本：扩展性[Essentials 2019](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ExtensibilityEssentials2019)或扩展性[Essentials 2022。](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ExtensibilityEssentials2022)

以下视频介绍所需的工具。

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RWPhtT]

## <a name="install-extensibility-workload"></a>安装扩展性工作负载

若要 **打开Visual Studio 安装程序，** 请选择"**工具**"，然后选择"**获取工具和功能..."。** 然后，安装 **Visual Studio扩展开发工作负载**。

:::image type="content" source="../media/visual-studio-installer.png" alt-text="显示扩展性工作负载的 VS Installer。":::

## <a name="install-extensibility-essentials"></a>安装扩展性 Essentials
若要安装 **扩展性 Essentials，** 请选择" **扩展"，** 选择" **管理** 扩展"，然后搜索 *扩展性*。

* 对于 Visual Studio 2019，请[安装 Extensibility Essentials 2019](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ExtensibilityEssentials2019)。
* 对于 Visual Studio 2022，请[安装 Extensibility Essentials 2022](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.ExtensibilityEssentials2022)。

:::image type="content" source="../media/install-extensibility-essentials.png" alt-text="从&quot;扩展管理器&quot;对话框中安装扩展性 Essentials。":::

这样，就可以开始开发第 [一个扩展了](first-extension.md)。
