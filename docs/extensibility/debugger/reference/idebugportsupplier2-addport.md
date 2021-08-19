---
description: 添加端口。
title: IDebugPortSupplier2：： AddPort |Microsoft Docs
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
ms.openlocfilehash: 581a805ad525f2cbcda95911b1620e7ccd773dfa
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132855"
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
中描述要添加的端口的 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 对象。

`ppPort`\
弄返回表示端口的 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法实际上会创建请求的端口，并将其添加到端口供应商的活动端口的内部列表。 可以首先调用 [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) 方法，以避免可能耗费时间的延迟。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
