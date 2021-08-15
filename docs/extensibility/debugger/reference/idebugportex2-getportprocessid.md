---
description: 获取端口本身的进程 ID。
title: IDebugPortEx2：：GetPortProcessId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2::GetPortProcessId
helpviewer_keywords:
- IDebugPortEx2::GetPortProcessId
ms.assetid: be85be66-47e6-415f-b0ca-24599aa5f13c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d90705ec4aee88e06209996fc47506ec23cf545e2132b37a245ef4bc111f0cd7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276940"
---
# <a name="idebugportex2getportprocessid"></a>IDebugPortEx2::GetPortProcessId
获取端口本身的进程 ID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortProcessId ( 
   DWORD* pdwProcessId
);
```

```csharp
int GetPortProcessId ( 
   out uint pdwProcessId
);
```

## <a name="parameters"></a>参数
`pdwProcessId`\
[out]返回端口本身的物理进程 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 例如，在 Win32 运行时中，此方法通常调用 Win32 函数 `GetCurrentProcessId` 获取物理进程 ID。

## <a name="see-also"></a>另请参阅
- [IDebugPortEx2](../../../extensibility/debugger/reference/idebugportex2.md)
