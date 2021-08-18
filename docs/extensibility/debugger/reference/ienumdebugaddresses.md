---
description: 此接口表示实现 IDebugAddress 接口的对象的集合。
title: IEnumDebugAddresses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: cfdb54c98728ff0c1eca2c2e4d455fdafc1e9419
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122137933"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
此接口表示实现 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由符号提供程序实现，以提供实现 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口的对象集。 请注意，由于存在 [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md) 方法，因此这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>调用方说明
 此接口由 [GetAddressesFromContext 和](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) [GetAddressesFromPosition 返回](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 此接口实现以下方法。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|从 枚举中检索 [下一组 IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|检索 枚举中的条目数。|

## <a name="remarks"></a>备注
 调试引擎通常使用此接口来帮助确定要赋予表达式计算程序的适当地址。

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
