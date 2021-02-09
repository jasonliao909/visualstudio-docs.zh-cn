---
title: IDebugThread2：： GetName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::GetName
helpviewer_keywords:
- IDebugThread2::GetName
ms.assetid: eec54b8f-4a0e-4919-b0f9-81d4bd1e0b6f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7a8a7a4f041e2a38cf1e24e8cf156d3e595010b6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99893849"
---
# <a name="idebugthread2getname"></a>IDebugThread2::GetName
获取线程的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetName ( 
   BSTR* pbstrName
);
```

```csharp
int GetName ( 
   out string pbstrName
);
```

## <a name="parameters"></a>parameters
`pbstrName`\
弄返回线程的名称。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 检索到的名称始终是一个可以显示的名称，此名称描述了该线程。 线程名称可能派生自支持命名线程的运行时结构，也可能是从调试引擎派生的名称。 或者，可以通过调用 [SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md) 方法来设置线程的名称。

## <a name="see-also"></a>另请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)
