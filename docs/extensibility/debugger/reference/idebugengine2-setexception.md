---
description: 指定调试引擎 (DE) 应如何处理给定的异常。
title: IDebugEngine2：：SetException |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetException
helpviewer_keywords:
- IDebugEngine2::SetException
ms.assetid: e6f5ec48-09e8-4b9b-9dc9-55f8d883f1b7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf8dea7fb30d51140b6445642865d71af08d78de
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602615"
---
# <a name="idebugengine2setexception"></a>IDebugEngine2::SetException
指定调试引擎 (DE) 应如何处理给定的异常。

## <a name="syntax"></a>语法

```cpp
HRESULT SetException( 
   EXCEPTION_INFO* pException
);
```

```csharp
int SetException( 
   EXCEPTION_INFO[] pException
);
```

## <a name="parameters"></a>parameters
`pException`\
[in]一 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 描述异常以及如何调试异常的异常结构。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 可以指示 DE 在出现第一次、第二次或完全不生成异常时停止程序。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
