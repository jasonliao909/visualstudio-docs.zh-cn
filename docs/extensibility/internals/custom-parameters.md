---
title: 自定义参数|Microsoft Docs
description: 了解如何通过修改 .vsz 文件，创建自定义参数来控制向导启动后向导的操作。
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
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: ec6cefad7714952e150a940e44c99741d6a9b98ed2267d38cab1651c69932b78
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448125"
---
# <a name="custom-parameters"></a>自定义参数
自定义参数控制向导启动后向导的操作。 相关的 *.vsz* 文件提供了一组用户定义参数，这些参数由集成开发环境 (IDE) 打包，在向导启动时作为字符串数组传递给向导。 然后，向导分析字符串数组，并使用信息来控制向导的实际操作。 这样，向导就可以根据 *.vsz* 文件的内容自定义功能。

 另一方面，上下文参数定义向导启动时项目的状态。 有关详细信息，请参阅 [上下文参数](../../extensibility/internals/context-parameters.md)。

 下面是具有自定义参数的 *.vsz* 文件的示例：

```
VSWIZARD 8.0
Wizard=VsWizard.VsWizard_Engine
Param="WIZARD_NAME = Sample Wizard"
Param="WIZARD_UI = FALSE"
Param="RELATIVE_PATH = VSWizards\Classwiz\ATL"
Param="PREPROCESS_FUNCTION = CanAddATLSupport"
Param="PROJECT_TYPE = CSPROJ"
```

 *.vsz 文件* 的作者添加参数的值。 当用户选择"新建Project"菜单上的"添加新项"或右键单击解决方案资源管理器 中的 **项目时**，IDE 将这些值收集到字符串数组中。  然后，IDE 调用设置了 标志的项目的 方法，项目将调用负责运行向导并 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3.AddItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.VSADDITEMOPERATION> <xref:EnvDTE.IVsExtensibility.RunWizardFile%2A> 返回结果的方法。

 向导负责分析字符串数组，并适当处理字符串。 这样，通过实现自定义参数，可以创建一个执行各种函数的向导。 换句话说，一个向导可以有三个不同的 *.vsz* 文件。 每个文件都传递不同的自定义参数集，以控制向导在各种情况下的行为。

 有关详细信息，请参阅向导 [ (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)。

## <a name="see-also"></a>另请参阅
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
