---
description: 此接口使表达式 (企业版) 可以调用值类实例的属性或方法 (例如 System.Decimal) ，并且无需对正在调试的程序调用 Evaluate 即可设置其值。
title: IDebugManagedObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject
helpviewer_keywords:
- IDebugManagedObject interface
ms.assetid: 3ae09d34-112c-4285-80ee-9f7f8dc414d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6cdf99a651f91d941aab00a732b6885300d092a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088466"
---
# <a name="idebugmanagedobject"></a>IDebugManagedObject
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口允许表达式 (企业版) 对值类实例调用属性或方法 (例如) ，并且无需对正在调试的程序调用 `System.Decimal` [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)即可设置其值。

## <a name="syntax"></a>语法

```
IDebugManagedObject : IDebugObject
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算程序实现此接口来表示托管代码对象，如变量。

## <a name="notes-for-callers"></a>调用方说明
 若要获取此接口，请对表示值类实例的[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)调用[GetManagedDebugObject。](../../../extensibility/debugger/reference/idebugobject-getmanageddebugobject.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了从 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)继承的方法之外， `IDebugManagedObject` 接口还公开了以下方法。

|方法|说明|
|------------|-----------------|
|[GetManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-getmanagedobject.md)|返回一个接口，该接口表示托管代码对象，可以从该对象获取任何适当的托管代码接口。|
|[SetFromManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject-setfrommanagedobject.md)|将此 对象的值设置为指定的托管代码对象的值。|

## <a name="remarks"></a>备注
 表达式计算程序使用此接口将托管代码对象存储在分析树中。

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [评估](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)
