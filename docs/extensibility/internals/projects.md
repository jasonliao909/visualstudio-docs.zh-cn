---
title: 项目|Microsoft Docs
description: 了解 VSPackage 扩展项目系统Visual Studio，包括项目类型、项目子类型和自定义工具。
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
ms.openlocfilehash: 2f0defdf43558cb94d3337a02d71ad768120da8c930244a9b03e1f05f6e75ee6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401279"
---
# <a name="projects"></a>项目
在 Visual Studio中，项目是开发人员用于组织源代码文件和显示在 中的其他资源的 **解决方案资源管理器。** 通常，项目是 (文件，例如，C# 项目的 .csproj 文件) 存储对源代码文件和资源（如位图文件）的引用。 使用项目可以组织、生成、调试和部署源代码、对 Web 服务和数据库的引用以及其他资源。 VSPackage 可以通过三Visual Studio扩展项目系统：项目类型、项目 *子类型和**自定义工具*。 

## <a name="in-this-section"></a>本节内容
- [项目类型](../../extensibility/internals/project-types.md)

 *Project类型* 添加了对新类型项目（如编程语言）的支持。 例如，Visual Studio支持的每种语言都有自己的项目类型，IronPython 集成示例包含 IronPython 语言的项目类型。 必须为 C# 或 Visual Basic语言创建项目类型，以自定义项的生成、调试、部署和显示方式 **解决方案资源管理器。** 有关详细信息，请参阅 Project[类型](../../extensibility/internals/project-types.md)。

- [项目子类型](../../extensibility/internals/project-subtypes.md)

 *Project子类型* 基于项目类型，可用于自定义项目的生成、调试和部署方式。 Visual Studio智能设备项目使用项目子类型;它们通过将新构建的程序从开发计算机复制到目标设备来自定义部署。 C# 和 Visual Basic项目类型可以用作项目子类型的基础;C++ 项目类型不能。 也可以将你自己的项目类型用作项目子类型的基础。 有关详细信息，请参阅子[Project类型](../../extensibility/internals/project-subtypes.md)。

- [Web 项目](../../extensibility/internals/web-projects.md)

 介绍 Web 项目，该项目又创建 Web 应用程序。

- [新Project代：在底层，](../../extensibility/internals/new-project-generation-under-the-hood-part-one.md)第一部分[和新Project代：在底层，第二部分](../../extensibility/internals/new-project-generation-under-the-hood-part-two.md)

 说明创建新项目时实际发生的情况。

- [VSSDK 示例](https://github.com/Microsoft/VSSDK-Extensibility-Samples) 包含 VSSDK 中处理项目和解决方案的示例。

## <a name="related-sections"></a>相关章节
- [深入探究 Visual Studio SDK](../../extensibility/internals/inside-the-visual-studio-sdk.md)

 说明扩展性Visual Studio方面。
