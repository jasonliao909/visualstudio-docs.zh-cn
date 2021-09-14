---
description: 获取引用的派生最多引用。
title: IDebugReference2：：GetDerivedMostReference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetDerivedMostReference
helpviewer_keywords:
- IDebugReference2::GetDerivedMostReference
ms.assetid: 07253b74-7d39-48e0-8e85-ac8dfd919f6e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e2980792572a6ac9c2d833a0fef62350db968d00
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664460"
---
# <a name="idebugreference2getderivedmostreference"></a>IDebugReference2::GetDerivedMostReference
获取引用的派生最多引用。 保留供将来使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDerivedMostReference( 
   IDebugReference2** ppDerivedMost
);
```

```csharp
int GetDerivedMostReference( 
   out IDebugReference2 ppDerivedMost
);
```

## <a name="parameters"></a>parameters
`ppDerivedMost`\
[out]返回一个 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象，该对象表示派生最多的属性。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL`。

## <a name="remarks"></a>备注
 例如，如果此属性描述实现 的对象，但实际上是派生自 的 实例化，则此方法返回表示对 对象的引用的 `ClassRoot` `ClassDerived` `ClassRoot` [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) `ClassDerived` 对象。

## <a name="see-also"></a>另请参阅
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
