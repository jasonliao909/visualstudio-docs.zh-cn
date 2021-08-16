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
ms.openlocfilehash: c2a10b0222e5ef5340b0d16b93d4dfb93289feee98e0de0e61f813febc0d000a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342175"
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

## <a name="parameters"></a>参数
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
