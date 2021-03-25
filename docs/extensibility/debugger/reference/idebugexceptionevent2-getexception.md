---
description: 获取引发此事件的异常的详细说明。
title: IDebugExceptionEvent2：： GetException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2::GetException
helpviewer_keywords:
- IDebugExceptionEvent2::GetException
ms.assetid: 7c98f41d-322b-4e72-a514-cbd4823eb70d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 72457b1b8931d028f555e7f9354f34b133fa79bb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084774"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
获取引发此事件的异常的详细说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetException( 
   EXCEPTION_INFO* pExceptionInfo
);
```

```csharp
int GetException( 
   EXCEPTION_INFO[] pExceptionInfo
);
```

## <a name="parameters"></a>参数
`pExceptionInfo`\
[in，out]一个 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 结构，其中填充了异常的说明。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注

 [仅限 c + +]调用方负责释放 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 结构中的任何字符串以及释放结构中的 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象。

## <a name="see-also"></a>另请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
