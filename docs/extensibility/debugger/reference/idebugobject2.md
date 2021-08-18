---
description: 此接口提供有关 对象的其他信息。
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
ms.openlocfilehash: d3d18068b5ad9ef74a84a31366d7c90bdefc365c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153285"
---
# <a name="idebugobject2"></a>IDebugObject2
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式计算器的方法已弃用。 有关实现 CLR 表达式评估器的信息，请参阅 [CLR 表达式评估器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式评估器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口提供有关 对象的其他信息。

## <a name="syntax"></a>语法

```
IDebugObject2 : IDebugObject
```

## <a name="notes-for-implementers"></a>实现者说明
 表达式计算程序实现此接口，以支持别名和访问有关对象的信息。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以使用[QueryInterface 获取此接口](/cpp/atl/queryinterface)。 此外 [，GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) 返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口上的方法外，该接口 `IDebugObject2` 还实现以下各项：

|方法|说明|
|------------|-----------------|
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|获取字段或变量 (如果) 支持此对象表示的属性的任何变量。|
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|获取表示此 对象的值的托管代码对象。|
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|为此对象创建唯一 ID 或返回现有别名。|
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|获取与此对象关联的别名（如果有）。|
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|获取此 对象的类型。|
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|确定此对象是否表示用户数据。|
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|确定"编辑并继续"状态是否不再有效。<br /><br /> 自定义表达式计算程序不会实现此方法 (它应始终返回 `E_NOTIMPL`) 。|

## <a name="remarks"></a>备注
 有关[别名的讨论，请参阅 IDebugAlias。](../../../extensibility/debugger/reference/idebugalias.md)

## <a name="requirements"></a>要求
 标头：ee.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
- [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
