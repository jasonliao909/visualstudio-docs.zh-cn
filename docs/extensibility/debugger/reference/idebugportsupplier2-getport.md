---
description: 从端口供应商获取端口。
title: IDebugPortSupplier2：：GetPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::GetPort
helpviewer_keywords:
- IDebugPortSupplier2::GetPort
ms.assetid: d55d5055-7386-4037-bf22-4c3e434a99ca
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d0c448c3c0a516180dfdc2422451b7c72cd7be804cd906c9f7c9bc2d82e7aedc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416815"
---
# <a name="idebugportsupplier2getport"></a>IDebugPortSupplier2::GetPort
从端口供应商获取端口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPort( 
   REFGUID       guidPort,
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   ref Guid        guidPort,
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>参数
`guidPort`\
[in]端口的 GUID (全局) 标识符。

`ppPort`\
[out]返回表示 [端口的 IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果 `E_PORTSUPPLIER_NO_PORT` 不存在具有给定标识符的端口，则返回 。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
