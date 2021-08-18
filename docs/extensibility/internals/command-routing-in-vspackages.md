---
title: VSPackages 中的命令|Microsoft Docs
description: 了解 VSPackage 中的命令路由，以及如何根据命令在 VSPackage 中执行的上下文路由Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, routing
- command routing, Visual Studio SDK
ms.assetid: a9c7f9ae-3594-4557-a314-8cf76f5f8772
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 71c662fc268a5db121a7699e97e1fa03c364a785
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122102813"
---
# <a name="command-routing-in-vspackages"></a>VSPackages 中的命令路由
根据执行 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 命令的上下文在 中路由命令。 它从初始上下文向外路由到全局上下文。

## <a name="in-this-section"></a>本节内容
- [命令路由算法](../../extensibility/internals/command-routing-algorithm.md)

 描述命令路由解析的顺序。

- [命令可用性](../../extensibility/internals/command-availability.md)

 讨论命令路由。

- [使用互操作程序集的命令和菜单](../../extensibility/internals/commands-and-menus-that-use-interop-assemblies.md)

 讨论在托管代码和 COM 之间路由命令的注意事项。

## <a name="related-sections"></a>相关章节
- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)

 讨论如何确定用户选择上下文焦点在窗口上的模型。

- [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)

 说明如何创建包含菜单、工具栏和命令组合框的 UI。
