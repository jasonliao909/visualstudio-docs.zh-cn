---
title: Project类型体系结构|Microsoft Docs
description: 本文链接到包含有关项目中项目类型体系结构的详细信息的文章Visual Studio。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], architecture
ms.assetid: 9c1d940f-8a54-41f7-a8aa-c870e324371c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: de1e6c30908db5d43540e5a93420095b636b76e0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122049722"
---
# <a name="project-types-architecture"></a>项目类型体系结构
本部分包含有关 中项目类型体系结构的详细信息 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="in-this-section"></a>本节内容
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)

 列出项目类型可以使用的服务及其必须实现接口。

- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)

 描述接口项目类型必须实现，并且（可选）可以实现以提供其他功能。

- [何时创建项目类型](../../extensibility/internals/when-to-create-project-types.md)

 帮助你决定何时必须创建项目类型，以及何时可以使用另一个扩展性功能（如 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] VSPackage 和编辑器）来实现相同的目标。

- [层次结构和选择](../../extensibility/internals/hierarchies-and-selection.md)

 描述 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 如何使用层次结构和选择上下文提供一致且简化的用户体验。

## <a name="related-sections"></a>相关章节
- [项目子类型](../../extensibility/internals/project-subtypes.md)

 说明项目子类型如何让你自定义 和 的项目系统 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 的行为 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 。

- [项目类型](../../extensibility/internals/project-types.md)

 概述作为 IDE 集成开发环境的基本构建基块 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 的项目 (IDE) 。 提供了其他主题的链接，这些主题介绍了项目如何控制代码的生成和编译。
