---
description: 此接口描述端口。
title: IDebugPortRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4c9ebd27ca070a8cc4f7d34099193356aa038811
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160005"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
此接口描述端口。 此说明用于将端口添加到端口供应商。

## <a name="syntax"></a>语法

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 Visual Studio通常在从端口供应商获取调试端口的过程中实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 此接口传递到 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 以创建调试端口。 对 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md) 的调用返回此接口，表示最初用于创建端口的请求。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugPortRequest2` 。

|方法|说明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|获取要创建的端口的名称。|

## <a name="remarks"></a>备注
 调试引擎通常不与端口供应商交互，并且不会用于此接口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
