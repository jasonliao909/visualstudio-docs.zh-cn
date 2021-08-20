---
description: 为此类的嵌套枚举器创建枚举器。
title: IDebugClassField：：EnumNestedEnums |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedEnums
helpviewer_keywords:
- IDebugClassField::EnumNestedEnums method
ms.assetid: 90fd0cef-9145-4de6-91d4-6c881df39d6e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ad0f51fa0874cf1068c097d20271a0b81178353
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127436"
---
# <a name="idebugclassfieldenumnestedenums"></a>IDebugClassField::EnumNestedEnums
为此类的嵌套枚举器创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumNestedEnums(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedEnums(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回表示 [嵌套枚举列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有嵌套枚举，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则S_OK，或者S_FALSE没有嵌套枚举器时返回值。 否则，返回错误代码。

## <a name="remarks"></a>备注
枚举的每个元素都是描述嵌套枚举 [的 IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md) 对象。

在类中声明的枚举被视为嵌套枚举。 例如，给定：

```
class RootClass {
    enum NestedEnum { EnumValue = 0 }
};
```

`EnumNestedEnums`方法将返回一个[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，该对象包含一个表示枚举的[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md) `NestedEnum` 对象。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
