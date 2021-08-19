---
description: 获取属性的派生程度最大的属性。
title: IDebugProperty2：： GetDerivedMostProperty |Microsoft Docs
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
ms.openlocfilehash: afa85a74a5104725f6712667317f8a5b8acfff0f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122132569"
---
# <a name="idebugproperty2getderivedmostproperty"></a>IDebugProperty2::GetDerivedMostProperty
获取属性的派生程度最大的属性。

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
弄返回表示最常派生的属性的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_GETDERIVEDMOST_NO_DERIVED_MOST`如果没有要检索的最常派生的属性，则返回。

## <a name="remarks"></a>备注
 例如，如果此属性描述一个对象，该对象实现， `ClassRoot` 但它实际上是 `ClassDerived` 派生自的实例 `ClassRoot` ，则此方法将返回描述对象的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象 `ClassDerived` 。

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
