---
description: 此接口提供对类型、别名和自定义可视化工具服务的访问。
title: IDebugBinder3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 5c34e3281857aa9f3a5edcbdf1e0822f2fb6bd13d77d62f0b02cbeecc1301de6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121308099"
---
# <a name="idebugbinder3"></a>IDebugBinder3
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供对类型、别名和自定义可视化工具服务的访问。

## <a name="syntax"></a>语法

```
IDebugBinder3 : IDebugBinder
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎实现此接口以支持别名、自定义可视化工具服务和访问对象类型信息。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)接口使用[QueryInterface 获取此接口](/cpp/atl/queryinterface)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口提供的方法外，此接口还实现以下各项：

|方法|说明|
|------------|-----------------|
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|检索一个内存对象，该对象表示此 对象绑定到的内存。|
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|检索与此对象关联的异常 (（如果有) ，|
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|根据别名检索别名，|
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|检索此 对象的所有别名的数组，|
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|获取与此 对象关联的参数类型的数量，|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|检索与此 对象关联的参数类型列表，|
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|获取可视化工具服务的接口，|
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|将对象位置或 64 位内存地址转换为内存上下文。|

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
