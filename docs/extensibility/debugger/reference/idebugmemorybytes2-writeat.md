---
description: 写入从指定地址开始的指定字节数。
title: IDebugMemoryBytes2：： WriteAt |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 099da50a72150d425fca560648df743f1804776f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600889"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
写入从指定地址开始的指定字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT WriteAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory
);
```

```csharp
int WriteAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory
);
```

## <a name="parameters"></a>parameters
`pStartContext`\
中 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象，指定开始写入字节的位置。

`dwCount`\
中要写入的字节数。

`rgbMemory`\
中要写入的字节数。 假定此数组的大小至少为 `dwCount` 个字节。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则， `S_FALSE` 如果不能写入所有字节，则返回; 否则返回错误代码 (通常 `E_FAIL`) 。

## <a name="remarks"></a>备注
 如果起始地址不在此 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) 对象所表示的内存窗口中，则不会执行任何写入操作，并且将返回错误代码 `E_FAIL` （即使要写入的量与内存空间重叠）。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
