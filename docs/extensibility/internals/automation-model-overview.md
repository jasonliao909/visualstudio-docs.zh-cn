---
title: 自动化模型概述|Microsoft Docs
description: 了解Visual Studio自动化模型，该模型由一组 对象组成，你可以针对这些对象编写Visual Studio或扩展。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- automation [Visual Studio SDK], about automation
- extensibility
ms.assetid: 12b6d6db-0d22-4aaa-aa7d-1365f759b7b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 24fdf3e87e4e8e58237052527e595bd60908373388d1e127f2607c88a609bfac
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121432758"
---
# <a name="automation-model-overview"></a>自动化模型概述
自动化模型由一组 对象组成，你可以针对这些对象编写Visual Studio或扩展。 外接程序是一个应用程序，它可以操作Visual Studio和自动执行常见任务。 一Visual Studio扩展可以创建自定义Visual Studio组件，或添加到标准组件（如文本编辑器）的功能。

## <a name="objects-in-the-automation-model"></a>自动化模型中的对象
 自动化模型由控制公共环境的主要方面的相关对象组组成。 下图显示了构成自动化模型的Visual Studio对象集。

 ![Visual Studio自动化对象图表](../../extensibility/internals/media/vsvisualstudioautomationobjectchart.gif "vsVisualStudioAutomationObjectChart")

 有关详细信息，请参阅[扩展Visual Studio环境](/previous-versions/esk3eey8(v=vs.140))。

 环境为不同的功能区域提供模型。 例如，在代码中可以找到各种元素的代码模型。 有一个适用于各种文档元素的文档模型。 VSPackage 提供程序特别感兴趣的一个领域是项目区域。 你可能希望新项目类型以与自动化模型相同的方式参与自动化模型并参与 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 自动化模型。 为 [VSPackage 提供自动化中概述了该过程](../../extensibility/internals/providing-automation-for-vspackages.md)。

 可以考虑扩展环境的自动化模型的位置：

- 项目

- 文档

- 代码

- 构建

有关自动化详细信息，请参阅自动化和扩展[性Visual Studio。](/previous-versions/visualstudio/visual-studio-2015/extensibility/extensibility-in-visual-studio?preserve-view=true&view=vs-2015) 本文档及其提供的链接可帮助你决定如何为 VSPackage 提供自动化。

## <a name="see-also"></a>另请参阅
- [如何：创建外接程序](/previous-versions/80493a3w(v=vs.140))