---
description: 获取以前用于创建端口 (（如果可用）) 的端口的说明。
title: IDebugPort2：： GetPortRequest |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortRequest
helpviewer_keywords:
- IDebugPort2::GetPortRequest
ms.assetid: 14abf847-0675-4fa8-872e-971e00c84224
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77224f98d953b61529ffed083e7be4cee0ed662f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087478"
---
# <a name="idebugport2getportrequest"></a>IDebugPort2::GetPortRequest
获取以前用于创建端口 (（如果可用）) 的端口的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortRequest( 
   IDebugPortRequest2** ppRequest
);
```

```csharp
int GetPortRequest( 
   out IDebugPortRequest2 ppRequest
);
```

## <a name="parameters"></a>参数
`ppRequest`\
弄返回一个 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 对象，该对象表示用于创建端口的请求。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。  `E_PORT_NO_REQUEST`如果未使用[IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)端口请求创建端口，则返回。

## <a name="see-also"></a>另请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
