---
description: 此接口提供了几种用于访问端口的服务器和通知设施的方法。
title: IDebugDefaultPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2
helpviewer_keywords:
- IDebugDefaultPort2 interface
ms.assetid: 7b3452af-9a96-4c4c-9946-4339b72d3d7b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: a606358b708b49f866063eeefc25b4e0c3fec44cab9fa8689492a475faeb3749
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417491"
---
# <a name="idebugdefaultport2"></a>IDebugDefaultPort2
此接口提供了几种用于访问端口的服务器和通知设施的方法。

## <a name="syntax"></a>语法

```
IDebugDefaultPort2 : IDebugPort2
```

## <a name="notes-for-implementers"></a>实现者说明
 Visual Studio此接口来表示用于访问程序调试端口。 如果自定义端口供应商处理远程调试，它也可以实现此接口。

## <a name="notes-for-callers"></a>调用方说明
 [IDebugProgramProvider2 接口](../../../extensibility/debugger/reference/idebugprogramprovider2.md)上的方法的参数提供此接口。 在[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)也可以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 除了 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)中定义的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetPortNotify](../../../extensibility/debugger/reference/idebugdefaultport2-getportnotify.md)|从此端口获取端口通知接口。|
|[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)|获取承载此端口的服务器接口。|
|[QueryIsLocal](../../../extensibility/debugger/reference/idebugdefaultport2-queryislocal.md)|确定此端口是否在本地计算机上运行。|

## <a name="remarks"></a>备注
 名称 `IDebugDefaultPort2` ""有点错误，因为它不表示默认端口。 它可称为"IDebugPort3"。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
