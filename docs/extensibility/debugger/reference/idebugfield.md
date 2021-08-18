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
ms.openlocfilehash: c38865ba18dfbc0020379a33c5becdb7440e406d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088752"
---
# <a name="idebugfield"></a>IDebugField
此接口表示一个字段，即符号或类型的说明。

## <a name="syntax"></a>语法

```
IDebugField : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序将此接口作为所有字段的基类实现。

## <a name="notes-for-callers"></a>调用方说明
 此接口是所有字段的基类。 根据 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)的返回值，此接口可能会使用 [QueryInterface](/cpp/atl/queryinterface)返回更多的专用接口。 此外，许多接口都返回 `IDebugField` 不同方法中的对象。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugField` 。

|方法|说明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)|获取有关符号或类型的可显示信息。|
|[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)|获取字段的类型。|
|[GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)|获取字段的类型。|
|[GetContainer](../../../extensibility/debugger/reference/idebugfield-getcontainer.md)|获取字段的容器。|
|[获取地址](../../../extensibility/debugger/reference/idebugfield-getaddress.md)|获取字段的地址。|
|[GetSize](../../../extensibility/debugger/reference/idebugfield-getsize.md)|获取字段的大小（以字节为单位）。|
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugfield-getextendedinfo.md)|获取有关字段的扩展信息。|
|[等于](../../../extensibility/debugger/reference/idebugfield-equal.md)|比较两个字段。|
|[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)|获取有关符号或类型的与类型无关的信息。|

## <a name="remarks"></a>备注
 类型等效于 C 语言 `typedef` 。

 在下面的 c + + 语言示例中， `weather` 是一个类类型，and `sunny` `stormy` 是符号：

```cpp
class weather;
weather sunny;
weather stormy;
```

 字段是否表示符号或类型，可以通过调用 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) 并检查 [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md) 结果来确定。 如果设置了位，则 `FIELD_KIND_TYPE` 字段为类型，如果 `FIELD_KIND_SYMBOL` 设置位，则为符号。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
