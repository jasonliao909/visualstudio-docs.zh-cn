---
description: 当已截获异常的处理完成时调用。
title: IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
helpviewer_keywords:
- IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
ms.assetid: 07b20866-e598-4783-9ecc-6aa8625c8804
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9892137ae9855097729fcd8482c2b1b3460152a2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118718"
---
# <a name="idebuginterceptexceptioncompleteevent2getinterceptcookie"></a>IDebugInterceptExceptionCompleteEvent2::GetInterceptCookie
当已截获异常的处理完成时调用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInterceptCookie(
   UINT64* pqwCookie
);
```

```csharp
int GetInterceptCookie(
   out ulong pqwCookie
);
```

## <a name="parameters"></a>参数
`pqwCookie`\
[out]与被截获的异常关联的唯一值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 在 [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) 方法完成已截获异常的处理后，它会发送 [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md) 事件。 处理程序可以使用 方法检索与异常关联的唯一值， (传递给方法的 `GetInterceptCookie` `InterceptCurrentException` 相同) 。

## <a name="see-also"></a>请参阅
- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)
- [IDebugInterceptExceptionCompleteEvent2](../../../extensibility/debugger/reference/idebuginterceptexceptioncompleteevent2.md)
