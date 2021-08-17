---
title: 使用安装程序安装程序Windows VSPackages |Microsoft Docs
description: 了解如何使用 Microsoft Windows 安装程序安装 VSPackage 及其依赖文件，以及如何注册并将其集成到 Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- installation [Visual Studio SDK], with Windows Installer
- VSPackages, deploying
ms.assetid: 41d2c72c-0a97-4fcd-b3aa-33a8d3aa962a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 63a0b57479ab8355031c9cf70df6caa1d19f2272865b380b431895dc856a4499
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121375946"
---
# <a name="installing-vspackages-with-windows-installer"></a>使用 Windows Installer 安装 VSPackage
将 VSPackage 集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中不仅需要将文件复制到用户的计算机。 VSPackage 的安装程序必须安装 VSPackage 及其依赖文件，并注册并将其集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中。 VSPackage 可以利用集成功能，如在初始屏幕上显示图标 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 和"关于"对话框。

 建议使用 Microsoft Windows 安装程序文件来分发 VSPackage。 易于使用的安装程序Windows可以在 支持的任何Windows操作系统中运行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 有关详细信息，请参阅 Windows[安装程序](/previous-versions/2kt85ked(v=vs.120))。

## <a name="in-this-section"></a>本节内容
- [Windows Installer 基本知识](../../extensibility/internals/windows-installer-basics.md)

 概述安装程序Windows安装程序。

- [VSPackage 安装方案](../../extensibility/internals/vspackage-setup-scenarios.md)

 讨论支持 VSPackage 和 的并行安装的不同方法 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [创作 Windows Installer 程序包](../../extensibility/internals/authoring-a-windows-installer-package.md)

 概述了安装程序正确安装 VSPackage 并将其集成到 中所遵循的典型步骤 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

- [检测系统要求](../../extensibility/internals/detecting-system-requirements.md)

 描述在未满足 VSPackage 要求时，安装程序如何检测及其组件 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 并取消设置。

- [组件管理](../../extensibility/internals/component-management.md)

 讨论如何开发一个安装程序，用于维护以前产品版本的完整性。

- [为 VSPackage 选择安装目录](../../extensibility/internals/choosing-the-installation-directory-for-a-vspackage.md)

 总结了用于定位 VSPackage 的选项。

- [VSPackage 注册](../../extensibility/internals/vspackage-registration.md)

 讨论在安装时如何注册 VSPackage，以及为什么自注册是一个坏想法。

- [部署项目类型](../../extensibility/internals/deploying-project-types.md)

 讨论如何将新的项目类型聚合器用于托管代码项目类型。

- [如何：生成安装程序的注册表信息](../../extensibility/internals/how-to-generate-registry-information-for-an-installer.md)

 说明如何使用 RegPkg.exe为托管 VSPackage 生成注册清单。

- [安装后必须运行的命令](../../extensibility/internals/commands-that-must-be-run-after-installation.md)

 说明如何运行安装后命令，将 VSPackage 集成到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 中。

- [使用 Windows Installer 卸载 VSPackage](../../extensibility/internals/uninstalling-a-vspackage-with-windows-installer.md)

 描述用户卸载 VSPackage 时安装程序必须执行的步骤。