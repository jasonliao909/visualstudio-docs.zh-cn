---
title: 实现 Single-File 生成器 |Microsoft Docs
description: '了解如何使用实现 IVsSingleFileGenerator 接口的自定义工具在 Visual Studio 中扩展 Visual Basic 和 Visual c # 项目系统。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom tools, implementing
- projects [Visual Studio SDK], extensibility
- projects [Visual Studio SDK], managed custom tools
ms.assetid: fe9ef6b6-4690-4c2c-872c-301c980d17fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: e9dd200879fb8a91eec5c63838d90f72dcad98b4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122069752"
---
# <a name="implementing-single-file-generators"></a>实现单个文件生成器
自定义工具（有时称为单个文件生成器）可用于 [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 在中扩展和项目系统 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 自定义工具是实现接口的 COM 组件 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 。 使用此接口，自定义工具将单个输入文件转换为一个输出文件。 转换的结果可以是源代码，也可以是任何有用的输出。 自定义工具生成的代码文件的两个示例是生成的代码，以响应可视化设计器中的更改和使用 Web 服务描述语言 (WSDL) 生成的文件。

 加载自定义工具或保存输入文件时，项目系统会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 方法，并传递对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsGeneratorProgress> 回调接口的引用，由此工具可向用户报告其进度。

 自定义工具生成的输出文件将添加到项目中，并对输入文件产生依赖关系。 项目系统根据自定义工具的实现返回的字符串，自动确定输出文件的名称 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> 。

 自定义工具必须实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator> 接口。 自定义工具还支持 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite> 从输入文件以外的源中检索信息的接口。 在任何情况下，你都必须将其注册到系统或本地注册表中，然后才能使用自定义工具 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 有关注册自定义工具的详细信息，请参阅 [注册单个文件生成器](../../extensibility/internals/registering-single-file-generators.md)。

## <a name="see-also"></a>请参阅
- [向可视化设计器公开类型](../../extensibility/internals/exposing-types-to-visual-designers.md)
