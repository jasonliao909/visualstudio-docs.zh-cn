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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ca2d1d59c66c87c2dbb0fc256481d35ad590dbe
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142617"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
此接口描述端口。 此描述用于向端口供应商添加端口。

## <a name="syntax"></a>语法

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 Visual Studio 通常在获取端口提供程序的调试端口的过程中实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 此接口将传递到 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 以创建调试端口。 对 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md) 的调用返回此接口，该接口表示首次创建端口时所用的请求。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugPortRequest2` 。

|方法|说明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|获取要创建的端口的名称。|

## <a name="remarks"></a>备注
 调试引擎通常不与端口供应商交互，并且不会使用此接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
