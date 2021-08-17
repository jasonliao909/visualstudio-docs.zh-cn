---
description: 在包含 (的对象Visual Basic) 指针中获取此对象。
title: IDebugMethodField：：GetThis |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 382b230e580ac09f81a3c23a3308c5b6c844fbcf04bb89dcb240001f7759b98f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433718"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
获取 `this` (`Me` 方法 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]) 的对象的指针中的对象。

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
[out]返回表示"this"指针的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 在面向对象的语言中，通常存在指向类的当前实例化的隐式指针。 这在 `this` C#/C++ 中称为 ，在 中 `Me` 称为 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
