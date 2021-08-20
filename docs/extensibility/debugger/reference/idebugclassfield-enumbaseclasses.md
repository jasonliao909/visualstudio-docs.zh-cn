---
description: 为此类的基类创建枚举器。
title: IDebugClassField：：EnumBaseClasses |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumBaseClasses
helpviewer_keywords:
- IDebugClassField::EnumBaseClasses method
ms.assetid: 78749674-ef75-46d3-a1f4-ff33afd90e32
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7bd7f742e057107e02d05934d62bab4747417588
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122145180"
---
# <a name="idebugclassfieldenumbaseclasses"></a>IDebugClassField::EnumBaseClasses
为此类的基类创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumBaseClasses( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumBaseClasses(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\

[out]返回表示 [基类列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有基类，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，S_SH_NO_BASE_CLASSES如果没有基类 (且 参数设置为 null 值，则返回 `ppEnum`) ;否则返回错误代码。

## <a name="remarks"></a>备注
 枚举器对象中的基类是按最直接的 (或派生) 到最远程基类的。 例如，给定 C++ 类：

```
class Root { }
class Level1 : Root { }
class Level2 : Level1 { }
class MyClass : Level2 { }
```

 枚举将按 、 、 的顺序返回 `Level2` 基 `Level1` 类 `Root` 。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
