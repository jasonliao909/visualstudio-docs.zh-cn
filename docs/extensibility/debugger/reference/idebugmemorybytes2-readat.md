---
description: 从给定位置开始读取字节序列。
title: IDebugMemoryBytes2：：ReadAt |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::ReadAt
helpviewer_keywords:
- IDebugMemoryBytes2::ReadAt method
- ReadAt method
ms.assetid: b413684d-4155-4bd4-ae30-ffa512243b5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6715129ad449e7d92ed2b74785469408973b25c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043435"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
从给定位置开始读取字节序列。

## <a name="syntax"></a>语法

```cpp
HRESULT ReadAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory,
   DWORD*                pdwRead,
   DWORD*                pdwUnreadable
);
```

```csharp
int ReadAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory,
   out uint             pdwRead,
   ref uint             pdwUnreadable
);
```

## <a name="parameters"></a>参数
`pStartContext`\
[in] [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象，指定开始读取字节的起始位置。

`dwCount`\
[in]要读取的字节数。 还指定数组 `rgbMemory` 的长度。

`rgbMemory`\
[in， out]用实际读取的字节填充的数组。

`pdwRead`\
[out]返回实际读取的连续字节数。

`pdwUnreadable`\
[in， out]返回不可读字节数。 如果客户端对不可读字节数没有关系，则该值可能为 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果请求 100 个字节且前 50 个字节是可读的，则接下来的 20 个不可读，其余 30 个字节是可读的，则此方法返回：

 *`pdwRead` = 50

 *`pdwUnreadable` = 20

 在这种情况下，由于 ，调用方必须额外调用 来读取原始请求的 100 个字节的剩余 30 个字节，并且参数中传递的 `*pdwRead + *pdwUnreadable < dwCount` [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象必须提前 `pStartContext` 70 个字节。

## <a name="see-also"></a>请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
