---
description: 确定此字段是否存在自定义属性，如果存在，则返回属性信息。
title: IDebugCustomAttributeQuery2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2
helpviewer_keywords:
- IDebugCustomAttributeQuery interface
- IDebugCustomAttributeQuery2 interface
ms.assetid: 7cfa23e4-a05a-47a3-af6c-bd40c655014b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 651bdf8b4bc9e43b5583855e3b1301e5fe4a2141fd5abeaae1483f169fcad8ec
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121262095"
---
# <a name="idebugcustomattributequery2"></a>IDebugCustomAttributeQuery2
确定此字段是否存在自定义属性，如果存在，则返回属性信息。

## <a name="syntax"></a>语法

```
IDebugCustomAttributeQuery2 : IDebugCustomAttributeQuery
```

## <a name="notes-for-implementers"></a>实现者说明
 符号提供程序在实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 的同一对象上实现此接口，以支持自定义属性。

## <a name="notes-for-callers"></a>调用方说明
 使用 [QueryInterface](/cpp/atl/queryinterface) 从 [IDebugField 接口获取此](../../../extensibility/debugger/reference/idebugfield.md) 接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 **IDebugCustomAttributeQuery 接口** 的方法。

|方法|说明|
|------------|-----------------|
|[IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)|确定自定义属性是否按名称存在。|
|[GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)|获取给定自定义属性的属性信息。|

 除了 **IDebugCustomAttributeQuery** 方法外 `IDebugCustomAttributeQuery2` ， 还实现以下方法：

|方法|说明|
|------------|-----------------|
|[EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)|获取附加到此字段的所有自定义属性的枚举器。|

## <a name="remarks"></a>备注
 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)方法可以返回为此字段定义的所有自定义属性的枚举器。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
