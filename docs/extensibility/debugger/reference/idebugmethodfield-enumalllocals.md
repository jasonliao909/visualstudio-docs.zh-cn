---
description: 为 方法的所有局部变量（包括编译器在内部生成的局部变量）创建枚举器。
title: IDebugMethodField：：EnumAllLocals |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9b31c956fa5cc94c8c595b5cf92f10498ea40a1ddb7fc5d4f2e830c3ea946d9d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307305"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
为 方法的所有局部变量（包括编译器在内部生成的局部变量）创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumAllLocals( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumAllLocals(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`pAddress`\
[in] [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象，表示 方法中的调试地址，指向特定范围或上下文。

`ppLocals`\
[out]返回一 [个 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示指定范围内所有局部变量的列表;否则， 将返回一个 null 值，指示没有局部值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，如果没有局部S_FALSE，则返回一个 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 仅枚举包含给定调试地址的 块中定义的变量。 此方法包括编译器生成的任何局部区域设置。 如果所需的全部内容是在源中显式定义的局部值，请调用 [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) 方法。

 方法可以包含多个范围上下文或块。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
