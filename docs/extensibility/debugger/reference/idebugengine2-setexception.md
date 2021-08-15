---
description: 指定调试引擎 (DE) 应如何处理给定的异常。
title: IDebugEngine2：： SetException |Microsoft Docs
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
ms.openlocfilehash: 62f2db9adf72a0029cbf693bd0388cf3483595e47f5b7f71036c759a8e37182e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390094"
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

## <a name="parameters"></a>参数
`pException`\
中描述异常以及如何调试异常的 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md) 结构。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 可以通过一种可能的取消，使程序在第一次机会、第二次机会或根本就停止生成异常。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)
