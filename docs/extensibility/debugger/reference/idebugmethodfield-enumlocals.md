---
description: 为方法的选定局部变量创建枚举器。
title: IDebugMethodField：：EnumLocals |Microsoft Docs
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
为方法的选定局部变量创建枚举器。

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
[in]表示 [调试地址的 IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象，该对象选择要从其中获取局部变量的上下文或作用域。

`ppLocals`\
[out]返回表示 [局部设置列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象;否则，如果没有局部值，则 返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回 S_OK，如果没有局部S_FALSE，则返回一个 。 否则，返回错误代码。

## <a name="remarks"></a>备注
仅枚举包含给定调试地址的 块中定义的变量。 如果需要所有局部区域，包括编译器生成的任何局部区域设置，请调用 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) 方法。

方法可以包含多个范围上下文或块。 例如，以下重试方法包含三个范围：两个内部块和方法主体本身。

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

[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)对象表示 `func` 方法本身。 例如 `EnumLocals` ，调用 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 设置为 地址的 方法将返回包含 变量 `Inner Scope 1` `temp1` 的枚举。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
