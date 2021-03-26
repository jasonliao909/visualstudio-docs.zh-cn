---
description: 此接口表示一个枚举类型。
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
ms.workload:
- vssdk
ms.openlocfilehash: 18671f8f719dc797709677a14417eaa0a54aaea2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105092522"
---
# <a name="idebugenumfield"></a>IDebugEnumField
此接口表示一个枚举类型。

## <a name="syntax"></a>语法

```
IDebugEnumField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序实现此接口来表示枚举。

## <a name="notes-for-callers"></a>调用方说明
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回，则使用[QueryInterface](/cpp/atl/queryinterface)从[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口获取此接口 `FIELD_TYPE_ENUM` 。

## <a name="methods-in-vtable-order"></a>VTable 顺序的方法
 除了和接口上的方法 `IDebugField` `IDebugContainerField` ，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetUnderlyingSymbol](../../../extensibility/debugger/reference/idebugenumfield-getunderlyingsymbol.md)|返回描述此枚举类型的名称的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 。|
|[GetStringFromValue](../../../extensibility/debugger/reference/idebugenumfield-getstringfromvalue.md)|返回与给定的值相关联的枚举常数的名称。|
|[GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)|返回与给定枚举常量名称关联的值|
|[GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)|返回与给定枚举常量名称关联的值，但忽略大小写。|

## <a name="remarks"></a>备注
 它是实际绑定到带有 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)的位置的基础符号。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [绑定](../../../extensibility/debugger/reference/idebugbinder-bind.md)
