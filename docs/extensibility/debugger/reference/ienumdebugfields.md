---
description: 此接口表示实现 IDebugField 接口的对象的集合。
title: IEnumDebugFields |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields
helpviewer_keywords:
- IEnumDebugFields interface
ms.assetid: 403c2a51-3ba5-431f-a1dd-2f3b2046c00c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 20fe0885186fefd2514be40e04cb27f3d92220c579f02f5679b48cabefde5c59
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415398"
---
# <a name="ienumdebugfields"></a>IEnumDebugFields
此接口表示实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口的对象的集合。

## <a name="syntax"></a>语法

```
IEnumDebugFields : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由符号提供程序实现，以提供实现 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口的对象集。 请注意，由于存在 [GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md) 方法，因此这不是标准 COM 枚举。

## <a name="notes-for-callers"></a>调用方说明
 此接口由 [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md) 和 [GetNamespacesUsedAtAddress 返回](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法
 此接口实现以下方法。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugfields-next.md)|从 枚举中检索 [下一组 IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugfields-skip.md)|跳过指定数量的条目。|
|[重置](../../../extensibility/debugger/reference/ienumdebugfields-reset.md)|将枚举重置为第一个条目。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugfields-clone.md)|检索当前枚举的副本。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugfields-getcount.md)|检索 枚举中的条目数。|

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [符号提供程序接口](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetMethodFieldsByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getmethodfieldsbyname.md)
- [GetNamespacesUsedAtAddress](../../../extensibility/debugger/reference/idebugsymbolprovider-getnamespacesusedataddress.md)
