---
title: IDebugProcess2：： GetProcessId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetProcessId
helpviewer_keywords:
- IDebugProcess2::GetProcessId
ms.assetid: d5b6f03c-d49d-4b83-b072-016ac3124f5f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df7b90d4096f651e0f055f9c92343df2a2712fe9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894889"
---
# <a name="idebugprocess2getprocessid"></a>IDebugProcess2::GetProcessId
获取此进程的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProcessId(
   GUID* pguidProcessId
);
```

```csharp
int GetProcessId(
   out Guid pguidProcessId
);
```

## <a name="parameters"></a>parameters
`pguidProcessId`\
弄返回此进程的 GUID。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 全局唯一标识符 (GUID) 从系统中运行的所有其他进程中标识此进程。

## <a name="see-also"></a>另请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
