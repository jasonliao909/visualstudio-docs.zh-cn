---
title: 实验实例|Microsoft Docs
description: 了解 Visual Studio SDK 如何提供试验性空间，以在调试模式下运行未经测试的应用程序。
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
为了Visual Studio开发环境，防止未经测试的应用程序更改它，VSSDK 提供了一个可用于试验的实验性空间。 你像往常一样使用 Visual Studio开发新应用程序，但通过使用此实验实例运行它们。

 每个具有 VSIX 包的应用程序都会在调试Visual Studio启动试验实例。

 如果要启动特定解决方案Visual Studio试验实例，请运行命令窗口中的以下命令：

 " *\<Visual studio installation path>* \Common7\IDE\devenv.exe" /RootSuffix Exp

> [!NOTE]
> 实验实例将写入 和 节点下的 `<version number>Exp` `<version number>Exp_Config` 注册表。 例如，Visual Studio 2015 试验注册表区域为
>
> `HKCU\Software\Microsoft\VisualStudio\14.0Exp` 和 `HKCU\Software\Microsoft\VisualStudio\14.0Exp_Config`

 建议在开发试验实例时在试验实例中运行扩展。 部署扩展时，该扩展在开发实例中运行。 有关注册应用程序的信息，请参阅[注册 VSPackage。](../extensibility/internals/registering-vspackages.md)
