---
title: 项目 |Microsoft Docs
description: 了解 vspackage 可以扩展 Visual Studio 项目系统的方式，包括项目类型、项目子类型和自定义工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions [Visual Studio]
- custom tools [Visual Studio SDK]
- project subtypes [Visual Studio SDK]
- projects [Visual Studio SDK]
- project types [Visual Studio SDK]
ms.assetid: 237742e4-a638-4d5b-a9b3-6a69d627763c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 9daeac1804940eb80331461b12b2cda51e9fef55
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602572"
---
# <a name="projects"></a>项目
在 Visual Studio 中，项目是开发人员用来组织 **解决方案资源管理器** 中出现的源代码文件和其他资源的容器。 通常，项目是文件 (例如，c # 项目的 .csproj 文件) 用于存储对源代码文件和资源（如位图文件）的引用。 项目使你可以组织、构建、调试和部署源代码，引用 Web 服务和数据库以及其他资源。 vspackage 可以通过以下三种主要方式扩展 Visual Studio 项目系统：*项目类型*、*项目子类型* 和 *自定义工具*。

## <a name="in-this-section"></a>本节内容
- [项目类型](../../extensibility/internals/project-types.md)

 *Project 类型* 添加了对新类型的项目（如编程语言）的支持。 例如，Visual Studio 支持的每种语言都有其自己的项目类型，IronPython 集成示例包含 IronPython 语言的项目类型。 您必须为 c # 或 Visual Basic 以外的语言创建项目类型，以自定义项目在 **解决方案资源管理器** 中的生成、调试、部署和显示方式。 有关详细信息，请参阅[Project 类型](../../extensibility/internals/project-types.md)。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 *Project 子* 类型基于项目类型，可用于自定义项目的生成、调试和部署方式。 Visual Studio 通过智能设备项目使用项目子类型;它们通过将新生成的程序从开发计算机复制到目标设备来自定义部署。 c # 和 Visual Basic 项目类型可用作项目子类型的基础;C + + 项目类型不能。 您自己的项目类型也可以用作项目子类型的基础。 有关详细信息，请参阅[Project 子类型](../../extensibility/internals/project-subtypes.md)。

- [Web 项目](../../extensibility/internals/web-projects.md)

 介绍 Web 项目，该项目将创建 Web 应用程序。

- [新 Project 生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)在幕后、第一代和[新 Project 生成：](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 说明创建新项目时实际发生的情况。

- [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples) 包含处理项目和解决方案的 VSSDK 中的示例。

## <a name="related-sections"></a>相关章节
- [深入探究 Visual Studio SDK](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 介绍 Visual Studio 扩展性的不同方面。
