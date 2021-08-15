---
description: 获取属性的派生最多的属性。
title: IDebugProperty2：：GetDerivedMostProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetDerivedMostProperty
helpviewer_keywords:
- IDebugProperty2::GetDerivedMostProperty
ms.assetid: cc86b461-62d1-4340-8209-c65037fd8b02
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8d202ba8594031cb72da1306e0828ef32423ac55c8cacfb58247ac6d373896b6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402488"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
获取属性的派生最多的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDerivedMostProperty ( 
   IDebugProperty2** ppDerivedMost
);
```

```csharp
int GetDerivedMostProperty ( 
   out IDebugProperty2 ppDerivedMost
);
```

## <a name="parameters"></a>参数
`ppDerivedMost`\
[out]返回一个 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象，该对象表示派生最多的属性。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 如果没有 `S_GETDERIVEDMOST_NO_DERIVED_MOST` 要检索的派生最多的属性，则返回 。

## <a name="remarks"></a>备注
 例如，如果此属性描述实现 的对象，但实际是派生自 的 实例化，则此方法返回描述该对象的 `ClassRoot` `ClassDerived` `ClassRoot` [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) `ClassDerived` 对象。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
