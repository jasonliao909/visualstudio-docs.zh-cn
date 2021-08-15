---
description: 添加端口。
title: IDebugPortSupplier2：：AddPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 87c7ed2bc53dcd793cb0c7c85ae3070f9236289e67d418c6b1ef3df9edd4e7d5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321813"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
添加端口。

## <a name="syntax"></a>语法

```cpp
HRESULT AddPort( 
   IDebugPortRequest2* pRequest,
   IDebugPort2**       ppPort
);
```

```csharp
int AddPort( 
   IDebugPortRequest2 pRequest,
   out IDebugPort2    ppPort
);
```

## <a name="parameters"></a>参数
`pRequest`\
[in]描述 [要添加的端口的 IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 对象。

`ppPort`\
[out]返回表示 [端口的 IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上创建请求的端口，并添加到端口供应商的活动端口的内部列表中。 可以 [先调用 CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) 方法，以避免可能耗时的延迟。

## <a name="see-also"></a>另请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
