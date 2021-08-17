---
description: 此接口表示一个自定义属性，它可以提供属性的名称、父类型和类类型。
title: IDebugCustomAttribute |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute
helpviewer_keywords:
- IDebugCustomAttribute interface
ms.assetid: c5ae41e9-00b9-4cca-871d-b8de9ef390d1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1007e82474093a04321bb3e550913fdc587f1dacf5d39c75ce9491c095588fb7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402930"
---
# <a name="idebugcustomattribute"></a>IDebugCustomAttribute
此接口表示一个自定义属性，它可以提供属性的名称、父类型和类类型。

## <a name="syntax"></a>语法

```
IDebugCustomAttribute : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序实现此接口，以便支持与符号关联的自定义特性。 它通常在自己的对象上实现。

## <a name="notes-for-callers"></a>调用方说明
 对 [下一次](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md) 的调用返回此接口。 调用 [EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md) 方法将返回 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) 接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugCustomAttribute` 。

|方法|说明|
|------------|-----------------|
|[GetParentField](../../../extensibility/debugger/reference/idebugcustomattribute-getparentfield.md)|获取当前特性附加到的字段。|
|[GetAttributeTypeField](../../../extensibility/debugger/reference/idebugcustomattribute-getattributetypefield.md)|获取自定义特性类类型。|
|[GetName](../../../extensibility/debugger/reference/idebugcustomattribute-getname.md)|获取自定义属性的名称。|
|[GetAttributeBytes](../../../extensibility/debugger/reference/idebugcustomattribute-getattributebytes.md)|获取作为字节 blob 的属性信息。|

## <a name="remarks"></a>备注
 自定义属性是 c # 的结构，它提供与特定类或方法关联的自定义元数据。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
