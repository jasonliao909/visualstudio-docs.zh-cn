---
title: 实验实例 |Microsoft Docs
description: 了解 Visual Studio SDK 如何在调试模式下提供试验性空间来运行未经测试的应用程序。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- experimental builds
- VSPackages, experimental builds
- VSIP, experimental builds
ms.assetid: ead0df4e-6f88-4b42-9297-581b7902f050
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 70f9d10595e1d0b458fc7102b48a1e1df8ee9daf6d2f04b993e7814891c41273
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121447605"
---
# <a name="the-experimental-instance"></a>实验实例
为了保护您的 Visual Studio 开发环境不受未经测试的应用程序的改变，VSSDK 提供了可用于试验的实验空间。 您可以像平常一样使用 Visual Studio 开发新应用程序，但使用此实验实例运行这些应用程序。

 具有 VSIX 包的每个应用程序在调试模式下启动 Visual Studio 的实验实例。

 如果要启动特定解决方案外 Visual Studio 的实验实例，请在命令窗口中运行以下命令：

 " *\<Visual studio installation path>* \Common7\IDE\devenv.exe"/RootSuffix Exp

> [!NOTE]
> 实验实例将写入到和节点下的注册表 `<version number>Exp` 中 `<version number>Exp_Config` 。 例如，Visual Studio 2015 试验性注册表区域是
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` 和 `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 建议你在开发时在实验实例中运行扩展。 部署扩展时，它在开发实例中运行。 有关注册应用程序的详细信息，请参阅 [注册 vspackage](../extensibility/internals/registering-vspackages.md)。
