---
description: 此接口描述数组符号或类型。
title: IDebugArrayField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6a14c4379abff21d97c5936914937f897942e010
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145453"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
此接口描述数组符号或类型。

## <a name="syntax"></a>语法

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口的同一对象上实现此接口。 此接口是表示数组对象的专用化。

## <a name="notes-for-callers"></a>调用方说明
 如果[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)返回标志 ，则使用[QueryInterface](/cpp/atl/queryinterface)从[IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)接口获取此接口 `FIELD_TYPE_ARRAY` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 和 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) 接口上的方法外，此接口还实现以下各项：

|方法|说明|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|获取数组中的元素数。|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|获取数组中元素的类型。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|获取数组的排名。|

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
