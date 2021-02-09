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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 728913596ce8c3947756906dffb144eecd3d71ca
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99895266"
---
# <a name="the-experimental-instance"></a>实验实例
为了保护你的 Visual Studio 开发环境不受未经测试的应用程序的可能更改，VSSDK 提供了一个试验空间，你可以使用它来试验。 您可以使用 Visual Studio 照常开发新应用程序，但使用此实验实例来运行它们。

 具有 VSIX 包的每个应用程序在调试模式下启动 Visual Studio 实验实例。

 如果要在特定解决方案外启动 Visual Studio 的实验实例，请在命令窗口中运行以下命令：

 " *\<Visual studio installation path>* \Common7\IDE\devenv.exe"/RootSuffix Exp

> [!NOTE]
> 实验实例将写入到和节点下的注册表 `<version number>Exp` 中 `<version number>Exp_Config` 。 例如，Visual Studio 2015 试验性注册表区域是
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` 和 `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 建议你在开发时在实验实例中运行扩展。 部署扩展时，它在开发实例中运行。 有关注册应用程序的详细信息，请参阅 [注册 vspackage](../extensibility/internals/registering-vspackages.md)。
