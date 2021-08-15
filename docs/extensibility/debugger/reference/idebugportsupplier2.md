---
description: 此接口向会话调试管理器提供端口 (SDM) 。
title: IDebugPortSupplier2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2
helpviewer_keywords:
- IDebugPortSupplier2 interface
ms.assetid: 37067324-2ea6-4a01-8829-a6e9c7a70068
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4a7280305b3241e2aa04fac3b47d6f73ba153e239ecc8eb12af94d3bdf7f196b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416763"
---
# <a name="idebugportsupplier2"></a>IDebugPortSupplier2
此接口向会话调试管理器提供端口 (SDM) 。

## <a name="syntax"></a>语法

```
IDebugPortSupplier2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
自定义端口供应商实现此接口来表示端口供应商。

## <a name="notes-for-callers"></a>调用方说明
使用端口供应商的 调用将返回此接口 (这是获取此接口的一种 `CoCreateInstance` `GUID`) 。 例如：

```cpp
IDebugPortSupplier2 *GetPortSupplier(GUID *pPortSupplierGuid)
{
    IDebugPortSupplier2 *pPS = NULL;
    if (pPortSupplierGuid != NULL) {
        CComPtr<IDebugPortSupplier2> spPortSupplier;
        spPortSupplier.CoCreateInstance(*pPortSupplierGuid);
        if (spPortSupplier != NULL) {
            pPS = spPortSupplier.Detach();
        }
    }
    return (pPS);
}
```

对 [GetPortSupplier 的](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md) 调用返回此接口，表示 所使用的当前端口供应商 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。

- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md) 返回此接口，表示创建端口的端口供应商。

- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md) 表示接口列表 (接口从 `IDebugPortSupplier` `IEnumDebugPortSuppliers` [EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)获取，表示向 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]) 注册的所有端口供应商。

调试引擎通常不与端口供应商交互。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
下表显示了 的方法 `IDebugPortSupplier2` 。

|方法|说明|
|------------|-----------------|
|[GetPortSupplierName](../../../extensibility/debugger/reference/idebugportsupplier2-getportsuppliername.md)|获取端口供应商名称。|
|[GetPortSupplierId](../../../extensibility/debugger/reference/idebugportsupplier2-getportsupplierid.md)|获取端口供应商标识符。|
|[GetPort](../../../extensibility/debugger/reference/idebugportsupplier2-getport.md)|从端口供应商获取端口。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugportsupplier2-enumports.md)|枚举已存在的端口。|
|[CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)|验证端口供应商是否支持添加新端口。|
|[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)|添加端口。|
|[RemovePort](../../../extensibility/debugger/reference/idebugportsupplier2-removeport.md)|删除端口。|

## <a name="remarks"></a>备注
端口供应商可以按名称和 ID 标识自身，添加和删除端口，并枚举端口供应商提供的所有端口。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugport2-getportsupplier.md)
- [GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
