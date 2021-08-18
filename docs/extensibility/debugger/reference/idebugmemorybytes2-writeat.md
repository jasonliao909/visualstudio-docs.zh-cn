---
description: 从指定的地址开始写入指定的内存字节数。
title: IDebugMemoryBytes2：：WriteAt |Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035015"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
从指定的地址开始写入指定的内存字节数。

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
[in] [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象，指定开始写入字节的起始位置。

`dwCount`\
[in]要写入的字节数。

`rgbMemory`\
[in]要写入的字节数。 假定此数组的大小至少为 `dwCount` 字节。

## <a name="return-value"></a>返回值
 如果成功，则 返回 ;否则，如果无法写入所有字节，则返回 ，或者返回错误代码 (`S_OK` `S_FALSE` 通常 `E_FAIL`) 。

## <a name="remarks"></a>备注
 如果起始地址不在[此 IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)对象表示的内存窗口中，则不会发生写入并返回错误代码 - 即使写入量与内存空间重叠。 `E_FAIL`

## <a name="see-also"></a>请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
