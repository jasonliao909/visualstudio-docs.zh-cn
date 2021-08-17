---
description: 表示函数并增强 IDebugFunctionObject 接口。
title: IDebugFunctionObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2 interface
ms.assetid: 56b2fdff-146d-4138-a34c-59a9c65a3ddd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 9bc2ebc0422dcffeb682f7ac9eb02216d5adf6505b1799d6f33c22e192aa184c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389769"
---
# <a name="idebugfunctionobject2"></a>IDebugFunctionObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示函数并增强 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口。

## <a name="syntax"></a>语法

```
IDebugFunctionObject2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算 (企业版) 实现此接口来表示函数。

## <a name="notes-for-callers"></a>调用方说明
 此接口的方法以下列方式延迟 **IDebugFunctionObject** 的方法：

- **IDebugEvaluate** 方法采用标志。

- **CreateObject** 方法采用标志和超时。

- **CreateStringObjectWithLength** 方法采用长度。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject2-createobject.md)|创建一个对象，该对象使用给定评估标志设置和超时值的构造函数。|
|[CreateStringObjectWithLength](../../../extensibility/debugger/reference/idebugfunctionobject2-createstringobjectwithlength.md)|创建具有指定长度的字符串对象。|
|[评估](../../../extensibility/debugger/reference/idebugfunctionobject2-evaluate.md)|调用 函数，将结果值作为 对象返回。|

## <a name="requirements"></a>要求
 标头：Ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
