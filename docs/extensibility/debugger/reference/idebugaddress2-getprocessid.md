---
description: 检索拥有此 IDebugAddress2 接口所表示的对象的进程的 ID。
title: IDebugAddress2：： GetProcessID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress2::GetProcessID
helpviewer_keywords:
- IDebugAddress2::GetProcessID method
ms.assetid: 2c18889d-074a-4b95-87b4-bf1a067f44ed
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fd7665af4f88c695dd74b51293da3eced3861230
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059192"
---
# <a name="idebugaddress2getprocessid"></a>IDebugAddress2::GetProcessID
检索拥有此 [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md) 接口所表示的对象的进程的 ID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProcessID (
   DWORD* pProcID
);
```

```csharp
int GetProcessID (
   out uint pProcID
);
```

## <a name="parameters"></a>参数
`pProcID`\
弄进程 ID。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugAddress2](../../../extensibility/debugger/reference/idebugaddress2.md)
