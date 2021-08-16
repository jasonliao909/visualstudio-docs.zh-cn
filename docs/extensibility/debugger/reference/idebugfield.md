---
description: 此接口表示一个字段，即符号或类型的说明。
title: IDebugField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField
helpviewer_keywords:
- IDebugField interface
ms.assetid: adecdd1c-b1b9-4027-92da-74cbe910636f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 24997c7dd1337c711f767a4af3e3dda454bb8459034801706abd68d006475c5d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389808"
---
# <a name="idebugfield"></a>IDebugField
此接口表示一个字段，即符号或类型的说明。

## <a name="syntax"></a>语法

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序将此接口实现为所有字段的基类。

## <a name="notes-for-callers"></a>调用方说明
 此接口是所有字段的基类。 根据 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)的返回值，此接口可能通过使用 [QueryInterface](/cpp/atl/queryinterface)返回更专用的接口。 此外，许多接口从 `IDebugField` 各种方法返回对象。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugField` 。

|方法|说明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|获取有关符号或类型的可显示信息。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|获取字段类型。|
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|获取字段的类型。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|获取 字段的容器。|
|[获取地址](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|获取字段的地址。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|获取字段的大小（以字节为单位）。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|获取有关字段的扩展信息。|
|[等于](../../../extensibility/debugger/reference/idebugfield-equal.md)|比较两个字段。|
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|获取有关符号或类型的与类型无关的信息。|

## <a name="remarks"></a>备注
 类型等效于 C 语言 `typedef` 。

 在下面的 C++ 语言示例中 `weather` ， 是类类型， `sunny` 和 `stormy` 是符号：

```cpp
class weather;
weather sunny;
weather stormy;
```

 字段是否表示符号或类型可以通过调用[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)并检查[FIELD_KIND确定。](../../../extensibility/debugger/reference/field-kind.md) 如果 `FIELD_KIND_TYPE` 设置了位，则字段为类型，如果 `FIELD_KIND_SYMBOL` 设置了位，则它是符号。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
