---
title: IDebugProcess3：： GetENCAvailableState |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetENCAvailableState
helpviewer_keywords:
- IDebugProcess3::GetENCAvailableState
ms.assetid: 98a5d527-8a72-476c-8e92-0bff3d97c195
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dce751223c4513733c5cd9ce815155b7f659b54a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915271"
---
# <a name="idebugprocess3getencavailablestate"></a>IDebugProcess3::GetENCAvailableState
此方法获取进程的当前编辑和继续状态。 自定义端口供应商应该总是返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```cpp
HRESULT GetENCAvailableState(
   EncUnavailableReason* pReason
);
```

```csharp
int GetENCAvailableState(
   EncUnavailableReason[] pReason
);
```

## <a name="parameters"></a>parameters
`pReason`\
弄 [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 枚举中的一个值。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

> [!NOTE]
> 自定义端口供应商应该总是返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注
 此状态可能受 [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)影响。

## <a name="see-also"></a>另请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
