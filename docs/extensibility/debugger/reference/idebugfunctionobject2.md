---
title: IDebugFunctionObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 304269ba2a4f556cfe931157c445d7b4fc86f489
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929935"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示函数并增强 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口。

## <a name="syntax"></a>语法

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器 (EE) 实现此接口来表示函数。

## <a name="notes-for-callers"></a>调用方说明
 此接口的方法通过以下方式将 **IDebugFunctionObject** 的方法延迟：

- **IDebugEvaluate** 方法采用标志。

- **CreateObject** 方法采用标志和超时。

- **CreateStringObjectWithLength** 方法使用长度。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|创建一个对象，该对象使用给定了计算标志设置和超时值的构造函数。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|创建一个具有指定长度的字符串对象。|
|[评估](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|调用函数并将生成的值作为对象返回。|

## <a name="requirements"></a>要求
 标头： Ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
