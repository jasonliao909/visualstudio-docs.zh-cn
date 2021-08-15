---
description: 检索此 IDebugMemoryBytes2 对象表示的内存大小（以字节为单位）。
title: IDebugMemoryBytes2：：GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::GetSize
helpviewer_keywords:
- IDebugMemoryBytes2::GetSize method
- GetSize method
ms.assetid: dae64c5f-5b54-40c3-b32f-ec3b16c093f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39a31c109f2d7d938e069cf5c1a91f1842ae2f2c6b29a822ed9bdf07969f4f2a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389678"
---
# <a name="idebugmemorybytes2getsize"></a>IDebugMemoryBytes2::GetSize
检索此 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) 对象表示的内存大小（以字节为单位）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   UINT64* pqwSize
);
```

```csharp
int GetSize(
   out ulong pqwSize
);
```

## <a name="parameters"></a>参数
`pqwSize`\
[out]返回内存空间的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
