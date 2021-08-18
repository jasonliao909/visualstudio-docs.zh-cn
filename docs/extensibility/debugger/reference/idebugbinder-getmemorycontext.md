---
description: 此方法将对象位置或内存地址转换为内存上下文。
title: IDebugBinder：：GetMemoryContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetMemoryContext
helpviewer_keywords:
- IDebugBinder::GetMemoryContext method
ms.assetid: 801c5b60-acff-4822-b23d-e9c7bbca8a0f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 48a4c9884f4625a938269715c5338d4040ccc8b3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119979"
---
# <a name="idebugbindergetmemorycontext"></a>IDebugBinder::GetMemoryContext
此方法将对象位置或内存地址转换为内存上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMemoryContext( 
   IDebugField*           pField,
   DWORD                  dwConstant,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int GetMemoryContext(
   IDebugField              pField,
   uint                     dwConstant,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>参数
`pField`\
[in]描述[要查找的对象的 IDebugField。](../../../extensibility/debugger/reference/idebugfield.md) 如果 `NULL` 为 ，则 `dwConstant` 改为使用 。

`dwConstant`\
[in]常量内存地址，例如0x5000。

`ppMemCxt`\
[out]返回 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 接口，该接口表示对象的地址或内存中的地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
