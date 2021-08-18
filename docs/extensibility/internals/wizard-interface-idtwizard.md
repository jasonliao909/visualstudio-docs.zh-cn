---
title: IDTWizard (向导接口) |Microsoft Docs
description: IDE 使用 IDTWizard 接口与向导通信。 向导必须实现此接口，以在 IDE 中安装。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-sdk
ms.workload:
- vssdk
ms.openlocfilehash: 08a1ec6e79624d3f1eb74f9b5251a73523a998c739c7ea215e3622643c5b9926
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121359138"
---
# <a name="wizard-interface-idtwizard"></a>向导界面 (IDTWizard)
IDE (集成) <xref:EnvDTE.IDTWizard> 使用 接口与向导通信。 向导必须实现此接口才能安装在 IDE 中。

 <xref:EnvDTE.IDTWizard.Execute%2A>方法是唯一与 接口关联的 <xref:EnvDTE.IDTWizard> 方法。 向导实现此方法，IDE 在 接口上调用 方法。 下面的示例演示 方法的签名。

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 "新建项"向导和"Project **项"向导的启动** 机制都类似。 若要启动任一操作，请调用 <xref:EnvDTE.IDTWizard> Dteinternal.h 中定义的 接口。 唯一的区别是调用接口时传递给接口的上下文参数和自定义参数集。

 以下信息描述了 <xref:EnvDTE.IDTWizard> 向导必须实现以在 IDE 中工作的 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 接口。 IDE 在 <xref:EnvDTE.IDTWizard.Execute%2A> 向导中调用 方法，并传递以下代码：

- DTE 对象

     DTE 对象是自动化模型的根。

- 窗口对话框的句柄，如代码段 所示 `hwndOwner ([in] long)` 。

     向导使用此 `hwndOwner` 作为向导对话框的父级。

- 作为 SAFEARRAY 的变体传递给接口的上下文参数，如代码段 中所示 `[in] SAFEARRAY (VARIANT)* ContextParams` 。

     上下文参数包含特定于正在启动的向导类型以及项目的当前状态的值数组。 IDE 将上下文参数传递给向导。 有关详细信息，请参阅 [上下文参数](../../extensibility/internals/context-parameters.md)。

- 作为 SAFEARRAY 的变体传递给接口的自定义参数，如代码段 中所示 `[in] SAFEARRAY (VARIANT)* CustomParams` 。

     自定义参数包含用户定义参数的数组。 .vsz 文件将自定义参数传递给 IDE。 值由 语句 `Param=` 确定。 有关详细信息，请参阅 [自定义参数](../../extensibility/internals/custom-parameters.md)。

- 接口的返回值为

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>请参阅
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
