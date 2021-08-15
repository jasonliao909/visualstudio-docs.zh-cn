---
description: 获取构成属性值的内存字节数。
title: IDebugProperty2：：GetMemoryBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryBytes
helpviewer_keywords:
- IDebugProperty2::GetMemoryBytes
ms.assetid: b32042ed-7a06-4b4a-99ef-fe03b0aa61cc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1acb73b3b24555193b02128a7ed557469f82fd219ba288029346e300d561dcc5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402449"
---
# <a name="idebugproperty2getmemorybytes"></a>IDebugProperty2::GetMemoryBytes
获取构成属性值的内存字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMemoryBytes ( 
   IDebugMemoryBytes2** ppMemoryBytes
);
```

```csharp
int GetMemoryBytes ( 
   out IDebugMemoryBytes2 ppMemoryBytes
);
```

## <a name="parameters"></a>参数
`ppMemoryBytes`\
[out]返回 [一个 IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) 对象，该对象可用于检索包含 属性的值的内存。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果没有 `S_GETMEMORYBYTES_NO_MEMORY_BYTES` 要检索的内存字节，则返回 。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
