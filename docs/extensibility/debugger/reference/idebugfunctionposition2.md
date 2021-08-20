---
description: 此接口表示函数在源文档中的抽象位置。
title: IDebugFunctionPosition2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionPosition2
helpviewer_keywords:
- IDebugFunctionPosition2 interface
ms.assetid: a835f65b-91b0-48ad-8485-04534c814b1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: ab8fd2348ce7c8e84e38d8b8029c23712620816b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064155"
---
# <a name="idebugfunctionposition2"></a>IDebugFunctionPosition2
此接口表示函数在源文档中的抽象位置。

## <a name="syntax"></a>语法

```
IDebugFunctionPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口来表示函数在源文档中的位置。

## <a name="notes-for-callers"></a>调用方说明
 此接口作为 BP_LOCATION 联合的一[](../../../extensibility/debugger/reference/bp-location.md) (提供，具体而言，BP_LOCATION_CODE_FUNC_OFFSET 结构) ，该结构又属于[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构的一部分，用于创建挂起断点。 [](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugFunctionPosition2` 。

|方法|说明|
|------------|-----------------|
|[GetFunctionName](../../../extensibility/debugger/reference/idebugfunctionposition2-getfunctionname.md)|获取此位置相对于的函数的名称。|
|[GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)|获取函数开头的偏移量。|

## <a name="remarks"></a>备注
 此接口表示的位置基于文本，具体而言，是[TEXT_POSITION结构。](../../../extensibility/debugger/reference/text-position.md)

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
