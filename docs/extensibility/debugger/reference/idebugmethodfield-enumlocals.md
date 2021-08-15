---
description: 为方法的选定局部变量创建枚举数。
title: IDebugMethodField：： EnumLocals |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2b9ea26c91f441ee5615e86bade7e1e412d59837e28d7fe3eedab06e715540c7
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339563"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
为方法的选定局部变量创建枚举数。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumLocals(
    IDebugAddress*     pAddress,
    IEnumDebugFields** ppLocals
);
```

```csharp
int EnumLocals(
    IDebugAddress        pAddress,
    out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`pAddress`\
中一个 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象，该对象表示一个调试地址，该地址选择从中获取局部变量的上下文或范围。

`ppLocals`\
弄返回表示局部变量列表的 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象;否则，如果没有局部变量，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回 S_OK 或返回 S_FALSE （如果没有局部变量）。 否则，返回错误代码。

## <a name="remarks"></a>备注
仅枚举包含给定调试地址的块中定义的变量。 如果需要所有局部变量，包括编译器生成的任何局部变量，请调用 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) 方法。

一个方法可以包含多个范围上下文或块。 例如，以下精心设计方法包含三个范围：两个内部块和方法体本身。

```csharp
public void func(int index)
{
    // Method body scope
    int a = 0;
    if (index == 1)
    {
        // Inner scope 1
        int temp1 = a;
    }
    else
    {
        // Inner scope 2
        int temp2 = a;
    }
}
```

[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)对象表示 `func` 方法本身。 `EnumLocals`例如，通过将[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)设置为 address 来调用方法将 `Inner Scope 1` 返回包含变量的枚举 `temp1` 。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
