---
title: 自定义参数 |Microsoft Docs
description: 了解如何创建自定义参数，以在向导启动后通过修改 .vsz 文件来控制向导的操作。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- wizards, custom parameters
- custom parameters
ms.assetid: ba5c364b-66e6-47ea-9760-a0b70de8f0a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3e5d8d9bf78f06dd55a88a2fbd47749224be3949
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091092"
---
# <a name="custom-parameters"></a>自定义参数
自定义参数用于在向导启动之后控制向导的操作。 相关的 *.vsz* 文件提供一个用户定义参数数组，这些参数由集成开发环境打包 (IDE) 并在启动向导时作为字符串数组传递到向导。 然后，该向导会分析字符串数组，并使用该信息来控制向导的实际操作。 通过这种方式，向导可以根据 *.vsz* 文件的内容自定义功能。

 另一方面，上下文参数在启动向导时定义项目的状态。 有关详细信息，请参阅 [上下文参数](../../extensibility/internals/context-parameters.md)。

 下面是包含自定义参数的 *.vsz* 文件的示例：

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.Vsz* 文件的作者添加参数的值。 当用户选择 "**文件**" 菜单上的 "**新建项目**" 或 "**添加新项**" 或在 **解决方案资源管理器** 中右键单击某个项目时，IDE 会将这些值收集到字符串数组中。 然后，IDE 将调用项目的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> 方法并 <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> 设置标志，并且项目将调用 <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> 负责运行向导并返回结果的方法。

 向导负责分析字符串数组，并对字符串进行适当的操作。 通过实现自定义参数，您可以创建一个向导来执行各种功能。 换言之，一个向导可能有三个不同的 *.vsz* 文件。 每个文件通过不同的自定义参数集来控制向导在各种情况下的行为。

 有关详细信息，请参阅 [向导 ( .vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 ( .vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
