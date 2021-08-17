---
description: 获取以前用于创建端口端口的端口的说明 (（如果) ）。
title: IDebugPort2：：GetPortRequest |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45afc09bea70a1b0f39cb7cdaa24ed24ab37ecb1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030329"
---
# <a name="idebugport2getportrequest"></a>IDebugPort2::GetPortRequest
获取以前用于创建端口端口的端口的说明 (（如果) ）。

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
[out]返回一 [个 IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 对象，该对象表示用于创建端口的请求。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。  如果未 `E_PORT_NO_REQUEST` 使用 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) 端口请求创建端口，则返回 。

## <a name="see-also"></a>请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
