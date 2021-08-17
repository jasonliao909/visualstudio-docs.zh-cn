---
description: 为 方法的静态局部变量创建枚举器。
title: IDebugMethodField：：EnumStaticLocals |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumStaticLocals
helpviewer_keywords:
- IDebugMethodField::EnumStaticLocals method
ms.assetid: e0c522c4-f759-4c32-ae87-7abcb573e77d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 05a1b7e5b0d00320bf74b04bf7f82534cdba7b5124d1e0241cb028995bd92609
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417049"
---
# <a name="idebugmethodfieldenumstaticlocals"></a>IDebugMethodField::EnumStaticLocals
为 方法的静态局部变量创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumStaticLocals( 
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumStaticLocals(
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`ppLocals`\
[out]返回表示 [静态局部变量列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有静态局部变量，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，如果没有静态局部S_FALSE，则返回一个 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是表示不同类型的静态局部变量的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象。 在每个 [对象上调用 GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md) 方法，以准确确定对象表示的静态本地类型。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
