---
description: 确定此字段的自定义特性是否存在，如果存在，则返回特性信息。
title: IDebugCustomAttributeQuery2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 62461cbdbfe373f6c3d45569564e611efdd6f452
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102160220"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
确定此字段的自定义特性是否存在，如果存在，则返回特性信息。

## <a name="syntax"></a>语法

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>实施者注意事项
 符号提供程序在实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 的同一对象上实现此接口，以便支持自定义属性。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 **IDebugCustomAttributeQuery** 接口的方法。

|方法|说明|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|确定是否存在按名称的自定义属性。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|获取给定自定义特性的特性信息。|

 除了 **IDebugCustomAttributeQuery** 方法，还 `IDebugCustomAttributeQuery2` 实现以下方法：

|方法|说明|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|获取附加到此字段的所有自定义属性的枚举器。|

## <a name="remarks"></a>备注
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)方法可以返回为该字段定义的所有自定义属性的枚举器。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
