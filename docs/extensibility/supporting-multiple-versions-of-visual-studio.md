---
title: 支持多个版本的Visual Studio |Microsoft Docs
description: 了解如何支持多个版本的 Visual Studio，使 VSPackage 能够加载到不同的版本。
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
" *并排"一* 词意味着你可以在同一计算机上安装和维护产品的多个版本。 对于 VSPackage，这意味着用户可以在同一计算机上Visual Studio多个版本。 但是，不能将 VSPackage 的并行版本加载到单个版本的 Visual Studio。

 在使 VSPackage 能够加载到并行版本的 Visual Studio 之前，请考虑以下事项：

- 必须确定要遵循的并行实现策略。

   有关详细信息，请参阅 [在共享 VSPackage 和版本控制 VSPackage 之间选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md)。

- 你的解决方案和项目文件格式必须适合你的实现策略。

   有关详细信息，请参阅 [升级自定义项目和](../extensibility/internals/upgrading-projects.md#upgrading-custom-projects) 为并行部署注册 [文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md)。

- 安装程序必须处理实现策略，以便正确安装和注册版本控制的组件以及所有版本之间共享的组件。

   有关详细信息，请参阅[Installing VSPackages with Windows 安装程序](../extensibility/internals/installing-vspackages-with-windows-installer.md)和[组件管理](../extensibility/internals/component-management.md)。

  > [!NOTE]
  > 安装版本 Visual Studio还会安装相应版本的 .NET Framework。 例如，在同一Visual Studio安装 Visual Studio 2010 和 Visual Studio 2012 也分别安装 .NET Framework 版本 4.0 和 4.5。

## <a name="in-this-section"></a>本节内容
- [在共享 VSPackage 和版本控制 VSPackage 之间选择](../extensibility/choosing-between-shared-and-versioned-vspackages.md) 说明如何解决 VSPackage 中的并行问题。

- [为并行部署注册文件扩展名](../extensibility/registering-file-name-extensions-for-side-by-side-deployments.md) 描述 VSPackage 如何在并行方案中注册文件关联。

## <a name="related-sections"></a>相关章节
- [使用 Windows Installer 安装 VSPackage](../extensibility/internals/installing-vspackages-with-windows-installer.md)
