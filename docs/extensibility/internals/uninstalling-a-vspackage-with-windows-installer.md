---
title: 使用安装程序安装程序Windows VSPackage |Microsoft Docs
description: Windows安装程序可以通过反转安装来卸载 VSPackage。 了解如何在安装程序包中处理Windows操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- packages, uninstalling
- VSPackages, uninstalling
- uninstalling VSPackages
ms.assetid: c4575ac7-82da-4af8-a375-ea756a101fbf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 688a438934f1b5a522e2fec211a4b134af143bcc40de4244f5538c5e084409b2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121414178"
---
# <a name="uninstalling-a-vspackage-with-windows-installer"></a>使用 Windows Installer 卸载 VSPackage
大多数情况下，Windows安装程序只需"撤消"安装 VSPackage 的操作，就可以卸载 VSPackage。 安装后必须运行的命令[](../../extensibility/internals/commands-that-must-be-run-after-installation.md)中讨论的自定义操作也必须在卸载后运行。 由于对 devenv.exe调用发生在 InstallFinalize 标准操作（用于安装和卸载）之前，CustomAction 和 InstallExecuteSequence 表条目适用于这两种情况。

> [!NOTE]
> 卸载 `devenv /setup` MSI 包后运行 。

 通常，如果将自定义操作添加到安装程序Windows包，则必须在卸载和回滚期间处理这些操作。 例如，如果添加自定义操作以自行注册 VSPackage，则必须添加自定义操作以取消注册它。

> [!NOTE]
> 用户可以安装 VSPackage，然后卸载集成它的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 版本。 通过消除在 上运行代码的自定义操作，可帮助确保 VSPackage 的卸载在这种情况下有效 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="handling-launch-conditions-at-uninstall-time"></a>在卸载时处理启动条件
 LaunchConditions 标准操作读取 LaunchCondition 表的行，以在条件不满足时显示错误消息。 由于启动条件通常用于确保满足系统要求，因此通常可以通过将条件 添加到 LaunchCondition 表的 LaunchConditions 行来跳过卸载期间启动 `NOT Installed` 条件。

 一种替代方法是 `OR Installed` 添加 以启动卸载过程中不重要的条件。 这可确保在卸载期间条件始终为 true，因此不会显示启动条件错误消息。

> [!NOTE]
> `Installed`是安装程序Windows VSPackage 已安装在系统时设置的属性。

## <a name="see-also"></a>请参阅
- [Windows Installer](/previous-versions/ee231230(v=vs.100))
- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)