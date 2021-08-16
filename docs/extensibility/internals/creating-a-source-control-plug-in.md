---
title: 创建源代码管理插件|Microsoft Docs
description: 了解如何创建源代码管理插件，将源代码管理功能添加到 IDE Visual Studio集成开发 (环境) 。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- plug-ins, source control
- source control plug-ins
- source control [Visual Studio SDK], plug-ins
ms.assetid: c7e69fa4-150e-469a-a6fc-fa1260bdbb07
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 495c04edfc85bacf50d2f7ba5440c27d17d08ed3c805f0f39d55408f6a6969a5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121305784"
---
# <a name="create-a-source-control-plug-in"></a>创建源代码管理插件
Visual Studio SDK 提供了一些资源，用于将源代码管理功能添加到 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE (集成) 。 它允许使用符合本文档中概述的源代码管理插件 API 的任何插件 DLL。

## <a name="in-this-section"></a>本节内容
- [入门](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

 介绍如何安装源代码管理插件，并突出显示当前可用的源代码管理插件 API 版本。

- [体系结构](../../extensibility/internals/source-control-plug-in-architecture.md)

 使用体系结构关系图说明源代码管理插件与 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 的集成。

- [测试指南](../../extensibility/internals/test-guide-for-source-control-plug-ins.md)

 提供有关如何测试源代码管理插件的安装和操作的指导。

## <a name="related-sections"></a>相关章节
- [创建源代码管理 VSPackage](../../extensibility/internals/creating-a-source-control-vspackage.md)

 讨论如何创建源代码管理 VSPackage，该 VSPackage 不仅提供源代码管理功能，还替换 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 源代码管理 UI。

- [源代码管理插件](../../extensibility/source-control-plug-ins.md)

 提供源代码管理插件 API 中所有元素的完整列表。

- [源代码管理](../../extensibility/internals/source-control.md)

 讨论将源代码管理作为 的集成功能实现的选项 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。
