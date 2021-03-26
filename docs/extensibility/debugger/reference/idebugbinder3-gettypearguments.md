---
description: 此方法检索与此对象关联的参数类型的列表。
title: IDebugBinder3：： GetTypeArguments |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetTypeArguments
helpviewer_keywords:
- IDebugBinder3::GetTypeArguments method
ms.assetid: fa0c37a7-327f-463e-9a9d-bb3f534584cb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cf360e85f4fdc2d641b00c6cd2252e58fa0d06cb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088999"
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
此方法检索与此对象关联的参数类型的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeArguments(
   UINT          skip,
   UINT          count,
   IDebugField** ppFields,
   UINT*         pFetched
);
```

```csharp
int GetTypeArguments(
   uint          skip,
   uint          count,
   IDebugField[] ppFields,
   out uint      pFetched
);
```

## <a name="parameters"></a>参数
`skip`\
中获取参数类型之前要跳过的字段数。

`count`\
中要返回的参数字段数 (还指定 `ppFields` 数组) 的大小。

`ppFields`\
[in，out]将在返回此方法时填充的字段数组。

`pFetched`\
[out] \(可选) 实际返回的参数类型字段的数目。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 可以事先通过 [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)获取参数类型的数目。

## <a name="see-also"></a>另请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)
