---
description: 此方法检索与此 对象关联的参数类型列表。
title: IDebugBinder3：：GetTypeArguments |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4fa3de2f8fc505aa6baaffd5c4370ef407c09029a33f9d2c2c14d02b8174f8e6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121262420"
---
# <a name="idebugbinder3gettypearguments"></a>IDebugBinder3::GetTypeArguments
此方法检索与此 对象关联的参数类型列表。

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
[in]获取参数类型之前要跳过的字段数。

`count`\
[in]要返回的参数字段 (还指定数组数组 `ppFields`) 。

`ppFields`\
[in， out]将在返回此方法时填充的字段数组。

`pFetched`\
[out] \(可选) 实际返回的参数类型字段数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 可以使用 [GetTypeArgumentCount 预先获取参数类型的数量](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)。

## <a name="see-also"></a>另请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)
