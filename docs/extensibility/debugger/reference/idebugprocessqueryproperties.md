---
description: 此接口是 IDebugProcess2 实现程序实现的扩展接口。
title: IDebugProcessQueryProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8205b96723a1b48da46e6e19162c50139c9fe71d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166211"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
此接口是 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 实现程序实现的扩展接口。 它允许实施者获取有关调试过程环境的信息。

## <a name="syntax"></a>语法

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 实现此接口可获取有关调试过程的执行环境的信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugProcessQueryProperties` 。

|方法|说明|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|查询属性值。|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|查询属性值。|

## <a name="remarks"></a>备注
 很少实现此接口。

## <a name="requirements"></a>要求
 标头： Portpriv

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
