---
description: 此接口是由 IDebugProcess2 实现程序实现的扩展接口。
title: IDebugProcessQueryProperties |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9dad8262b2c8add1787d07dbd4589c2398d9c807abef5aaa06fc3ba46244f193
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433406"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
此接口是由 [IDebugProcess2 实现程序实现的](../../../extensibility/debugger/reference/idebugprocess2.md) 扩展接口。 它允许实现者获取有关调试进程环境的信息。

## <a name="syntax"></a>语法

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 实现此接口可获取有关调试进程的执行环境的信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProcessQueryProperties` 。

|方法|说明|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|对属性值的查询。|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|属性值的查询。|

## <a name="remarks"></a>备注
 此接口很少实现。

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
