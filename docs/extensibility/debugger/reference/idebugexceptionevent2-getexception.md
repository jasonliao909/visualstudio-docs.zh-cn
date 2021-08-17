---
description: 获取触发此事件的异常的详细说明。
title: IDebugExceptionEvent2：：GetException |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7da0fc91cd32ffedbf36f98f736c99db21c7a2e1904fe8af6aec2dec323e309
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121292528"
---
# <a name="idebugexceptionevent2getexception"></a>IDebugExceptionEvent2::GetException
获取触发此事件的异常的详细说明。

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
[in， out]一 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 用异常说明填充的异常结构。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注

 [仅 C++]调用方负责释放结构中 [EXCEPTION_INFO字符串，](../../../extensibility/debugger/reference/exception-info.md) 以及释放 [结构中 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 对象。

## <a name="see-also"></a>请参阅
- [IDebugExceptionEvent2](../../../extensibility/debugger/reference/idebugexceptionevent2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
