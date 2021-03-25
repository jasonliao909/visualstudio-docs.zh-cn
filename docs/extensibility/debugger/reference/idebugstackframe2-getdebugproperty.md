---
description: 获取堆栈帧的属性的说明。
title: IDebugStackFrame2：： GetDebugProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetDebugProperty
helpviewer_keywords:
- IDebugStackFrame2::GetDebugProperty
ms.assetid: 02c2fa04-1424-4bca-9936-feaecd2afab6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5c4017e5a14619c2ab5e3f98de65d7d2295e8586
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053472"
---
# <a name="idebugstackframe2getdebugproperty"></a>IDebugStackFrame2::GetDebugProperty
获取堆栈帧的属性的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDebugProperty ( 
   IDebugProperty2** ppDebugProp
);
```

```csharp
int GetDebugProperty ( 
   out IDebugProperty2 ppDebugProp
);
```

## <a name="parameters"></a>参数
`ppDebugProp`\
弄返回描述此堆栈帧的属性的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通过适当的筛选器调用 [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) 方法可以检索与堆栈帧关联的局部变量、方法参数、寄存器和 "this" 指针。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
