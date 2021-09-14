---
title: 向可视化设计器公开类型|Microsoft Docs
description: 了解如何公开类和类型定义，包括自定义工具中的定义，以便Visual Studio设计器可以使用它们。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- types [Visual Studio SDK], exposing to visual designers
- designers [Visual Studio SDK], exposing types
- custom tools, exposing types to visual designers
ms.assetid: a7a32ad4-3a0a-4eb8-a6ac-491c42885639
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ffee5f17192cc14346f9da52ce32551dea6daded
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664379"
---
# <a name="expose-types-to-visual-designers"></a>向可视化设计器公开类型
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 在设计时必须有权访问类和类型定义才能显示可视化设计器。 从预定义的程序集集加载类，这些程序集包括当前项目的完整依赖项集 (引用及其依赖项) 。 可视化设计器可能还需要访问自定义工具生成的文件中定义的类和类型。

 和 项目系统支持通过临时可移植可执行文件访问生成的类和 ([!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 临时 PE) 。 自定义工具生成的任何文件都可以编译为临时程序集，以便可以从这些程序集加载类型并公开给设计器。 每个自定义工具的输出都编译为单独的临时 PE，此临时编译的成功或失败仅取决于是否可以编译生成的文件。 即使项目可能不会作为一个整体生成，各个临时 PES 仍可供设计人员使用。

 项目系统完全支持跟踪自定义工具的输出文件更改，但这些更改是运行自定义工具的结果。 每次运行自定义工具时，会生成一个新的临时 PE，并且会向设计器发送相应的通知。

> [!NOTE]
> 由于临时程序可执行文件生成文件在后台发生，因此编译失败时不会向用户报告任何错误。

 利用临时 PE 支持的自定义工具必须遵循以下规则：

- **GeneratesDesignTimeSource** 必须在注册表中设置为 1。

     如果没有此设置，则不进行程序可执行文件编译。

- 生成的代码必须与全局项目设置的语言相同。

     如果 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.DefaultExtension%2A> **GeneratesDesignTimeSource** 在注册表中设置为 1，则编译临时 PE，而不考虑自定义工具在 中报告为请求的扩展。 该扩展不需要为 *.vb、.cs* 或 *.jsl*; 可以是任何扩展。

- 自定义工具生成的代码必须有效，并且它必须使用执行时项目中存在的引用集自行 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSingleFileGenerator.Generate%2A> 编译。

     编译临时 PE 时，提供给编译器的唯一源文件是自定义工具输出。 因此，使用临时 PE 的自定义工具必须生成可以独立于项目中其他文件编译的输出文件。

## <a name="see-also"></a>另请参阅
- [BuildManager 对象简介](/previous-versions/8f9kffa8(v=vs.140))
- [实现单文件生成器](../../extensibility/internals/implementing-single-file-generators.md)
- [注册单文件生成器](../../extensibility/internals/registering-single-file-generators.md)