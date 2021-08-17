---
title: 层次结构和选择|Microsoft Docs
description: 了解如何Visual Studio层次结构（如项目）以及它如何使用选择上下文来确定向用户显示的内容。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, hierarchies
- selection
- hierarchies
ms.assetid: cad0a859-7a84-4ce5-b0a9-f7f64e5f8ebb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 77ca0dbfd8476aae3b7dc8a12a0a449eb074da4480aa2f2546bc12c7282690ce
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121376178"
---
# <a name="hierarchies-and-selection"></a>层次结构和选择
自定义 时，应了解如何处理层次结构（如项目）以及它如何使用选择上下文来确定 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 向用户显示的内容。 本部分讨论层次结构 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 和选择的概念。

## <a name="in-this-section"></a>本节内容
- [Visual Studio 中的层次结构](../../extensibility/internals/hierarchies-in-visual-studio.md)

 介绍项目层次结构和层次结构的一般概念。

- [IDE 中的选择和货币](../../extensibility/internals/selection-and-currency-in-the-ide.md)

 介绍集成开发环境 (IDE) 如何维护有关用户当前活动对象的信息，并允许 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackages 跟踪货币。

- [选择上下文对象](../../extensibility/internals/selection-context-objects.md)

 讨论如何确定用户选择上下文焦点在窗口上的模型。

- [向用户反馈](../../extensibility/internals/feedback-to-the-user.md)

 讨论 中的可用功能如何基于用户的当前选择 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 上下文和整体 IDE 上下文。

## <a name="related-sections"></a>相关章节
- [Project类型体系结构](../../extensibility/internals/project-types-architecture.md)

 提供有关项目类型的详细技术信息。
