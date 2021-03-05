---
description: 创建嵌套在此类中的类的枚举器。
title: IDebugClassField：： EnumNestedClasses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 87538db39df590fd3885f545e5442c7dafecb9a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164261"
---
# <a name="idebugclassfieldenumnestedclasses"></a>IDebugClassField::EnumNestedClasses
创建嵌套在此类中的类的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumNestedClasses(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedClasses(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回一个 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示嵌套类的列表。 如果没有嵌套类，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回 S_OK 或返回 S_FALSE （如果没有嵌套类）。 否则，返回错误代码。

## <a name="remarks"></a>备注
枚举的每个元素都是一个描述嵌套类的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。

嵌套类是在另一个类中定义的类。 例如：

```
class RootClass {
   class NestedClass { }
};
```

[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)枚举将包含一个表示类的对象 `NestedClass` 。

## <a name="see-also"></a>另请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
