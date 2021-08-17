---
title: 自定义工具|Microsoft Docs
description: 了解如何在文件中创建自定义工具Visual Studio将工具与项目中的项关联，并每次保存文件时运行该工具。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, custom tools
- tools [Visual Studio], custom
- custom tools
ms.assetid: d669f154-9b23-48b6-b9f6-7419c8dd61a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: f94710fea84201af2a89dc1ce609e0de7588f0c9
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122094953"
---
# <a name="custom-tools"></a>自定义工具
*使用自定义* 工具可以将工具与项目中的项关联，并每次保存文件时运行该工具。 某些自定义工具（有时称为单文件生成器）通常用于实现从数据生成代码的转换器，反之亦然。 例如，单文件生成器从 .settings 和 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] *.resx* 文件创建和源代码。  生成的源代码提供对 *.settings* 和 *.resx* 文件中数据的强类型访问。 和 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] 项目类型支持自定义工具; [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目类型不支持。 你自己的项目类型还可以支持自定义工具。

 自定义工具是实现 接口的已注册 `IVsSingleFileGenerator` 组件。

 自定义工具与接口 `ProjectItem` 对象相关联，与设计器和编辑器类似。 自定义工具将 表示的文件用作输入，并写入其文件名由 方法 `ProjectItem` 提供的新 `DefaultExtension` 文件。

## <a name="in-this-section"></a>本节内容
- [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)

 介绍如何使用 接口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 实现自定义工具。

- [注册单文件生成器](../../extensibility/internals/registering-single-file-generators.md)

 提供自定义工具的所有注册表项的说明。

- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)

 介绍项目系统如何支持可视化设计器通过 PE 文件的临时可移植可执行文件 (生成的类) 类型。

- [保留项目项的 属性](../../extensibility/persisting-the-property-of-a-project-item.md)

 演示如何在项目文件中保留项目项属性，例如源文件的作者。

## <a name="reference"></a>参考
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 提供有关 的详细信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> ，该文件将单个输入文件转换为可以编译或添加到项目的单个输出文件。

 <xref:EnvDTE.ProjectItem> 说明 `ProjectItem` 接口，该接口表示项目中的项。

 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 提供有关 方法的详细信息，该方法检索为输出文件名 `DefaultExtension` 提供的文件扩展名。

## <a name="related-sections"></a>相关章节
- [扩展项目](../../extensibility/extending-projects.md)

 介绍如何使用 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 项目和解决方案来组织代码文件和资源文件，以及如何实现源代码管理。
