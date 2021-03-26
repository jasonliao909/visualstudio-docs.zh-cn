---
description: 获取此 (我在包含方法的对象 Visual Basic) 指针中。
title: IDebugMethodField：： GetThis |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetThis
helpviewer_keywords:
- IDebugMethodField::GetThis method
ms.assetid: cc235bea-e909-4d8c-ab54-936736c803fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 662555ec4552aa016b40c1e9c8222992e6cdfd66
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076636"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
获取 `this` `Me` [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 包含方法的对象) 指针中的 (。

## <a name="syntax"></a>语法

```cpp
HRESULT GetThis( 
   IDebugClassField** ppClass
);
```

```csharp
int GetThis(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>参数
`ppClass`\
弄返回表示 "this" 指针的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 在面向对象的语言中，通常是指向类的当前实例化的隐含指针。 这 `this` 在 c #/c + + 中称为，如 `Me` 中所示 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
