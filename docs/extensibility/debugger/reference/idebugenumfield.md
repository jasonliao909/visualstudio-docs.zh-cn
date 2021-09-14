---
description: 此接口表示枚举类型。
title: IDebugEnumField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField
helpviewer_keywords:
- IDebugEnumField interface
ms.assetid: 42f685bf-0f39-47f4-98b0-6022efe2bf97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: fb8cb02d178a9efcb9b3d03423b722a4950c6511
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602427"
---
# <a name="idebugenumfield"></a>IDebugEnumField
此接口表示枚举类型。

## <a name="syntax"></a>语法

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序实现此接口来表示枚举。

## <a name="notes-for-callers"></a>调用方说明
 如果 GetKind 返回 ，则使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口 [获取此](../../../extensibility/debugger/reference/idebugfield-getkind.md) 接口 `FIELD_TYPE_ENUM` 。

## <a name="methods-in-vtable-order"></a>VTable 顺序中的方法
 除了 和 接口上 `IDebugField` `IDebugContainerField` 的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|返回描述此枚举类型的名称的[IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|返回与给定值关联的枚举常量的名称。|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|返回与给定枚举常量名称关联的值|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|返回与给定枚举常量名称关联的值，但忽略大小写。|

## <a name="remarks"></a>备注
 它是实际绑定到具有绑定 的位置的基础 [符号](../../../extensibility/debugger/reference/idebugbinder-bind.md)。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)
