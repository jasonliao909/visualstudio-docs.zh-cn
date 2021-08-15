---
title: 支持 Visual Studio 的多个版本 |Microsoft Docs
description: 了解如何支持 Visual Studio 的多个版本，vspackage 可以将其加载到不同版本。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, supporting multiple versions
- VSPackages, side-by-side compatibility
ms.assetid: 0047aa90-1ed4-40d3-8772-622b2719a4b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 4e0624461d6f37468c0d44ace6c287bda67021bcbef7c525dd871dab691cf282
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121413825"
---
# <a name="supporting-multiple-versions-of-visual-studio"></a>支持多个版本的 Visual Studio
*术语 "并排"* 表示可以在同一台计算机上安装和维护产品的多个版本。 对于 vspackage，这意味着用户可以在同一台计算机上安装多个 Visual Studio 版本。 但是，你不能将 Vspackage 的并行版本加载到 Visual Studio 的单个版本。

 在将 VSPackage 加载到 Visual Studio 的并行版本之前，请考虑以下事项：

- 你必须确定要遵循的并行实现策略。

   有关详细信息，请参阅 [在 Shared 和 Vspackage 之间进行选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md)。

- 解决方案和项目文件格式必须符合实现策略。

   有关详细信息，请参阅 [升级自定义项目](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects) 和 [注册并行部署的文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 安装程序必须处理实现策略，以便正确安装和注册已进行版本控制的组件以及跨所有版本共享的组件。

   有关详细信息，请参阅将[vspackage 与 Windows Installer](../extensibility/internals/installing-vspackages-with-windows-installer.md)和[组件管理](../extensibility/internals/component-management.md)一起安装。

  > [!NOTE]
  > 安装 Visual Studio 版本也会安装相应版本的 .NET Framework。 例如，在同一台计算机上安装 Visual Studio 2010 和 Visual Studio 2012 还将分别安装 .NET Framework 的版本4.0 和4.5。

## <a name="in-this-section"></a>本节内容
- [在共享和版本控制之间进行选择 vspackage](../extensibility/choosing-between-shared-and-versioned-vspackages.md) 说明如何在 VSPackage 中解析并行问题。

- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) 介绍 VSPackage 如何在并行方案中注册文件关联。

## <a name="related-sections"></a>相关章节
- [使用 Windows Installer 安装 VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)
