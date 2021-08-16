---
description: 此接口提供有关对象的其他信息。
title: IDebugObject2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c1d828f63508ff11f013857f4a7214c0f37cb60ab905d437a4bf707221bd0108
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433445"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供有关对象的其他信息。

## <a name="syntax"></a>语法

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器实现此接口，以提供对别名的支持以及对对象信息的访问。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以使用[QueryInterface](/cpp/atl/queryinterface)获取此接口。 此外， [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) 返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口上的方法之外， `IDebugObject2` 接口还实现以下各项：

|方法|说明|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|如果任何可能支持此对象所表示的属性的) ，则获取字段或变量 (。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|获取表示此对象的值的托管代码对象。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|为此对象创建唯一 ID，或返回现有别名。|
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|获取与此对象关联的别名（如果有）。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|获取此对象的类型。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|确定此对象是否表示用户数据。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|确定 "编辑并继续" 状态是否不再有效。<br /><br /> 自定义表达式计算器不实现此方法 (应始终返回 `E_NOTIMPL`) 。|

## <a name="remarks"></a>备注
 有关别名的讨论，请参阅 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 。

## <a name="requirements"></a>要求
 标头： ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
