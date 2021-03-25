---
description: 获取附加到此字段的所有自定义属性的枚举器。
title: IDebugCustomAttributeQuery2：： EnumCustomAttributes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
helpviewer_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
ms.assetid: 94bfce74-aa3d-45f0-8e04-5715faf85217
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5bcd11f3058de191a3b0a77f0316afb6140769fc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077637"
---
# <a name="idebugcustomattributequery2enumcustomattributes"></a>IDebugCustomAttributeQuery2::EnumCustomAttributes
获取附加到此字段的所有自定义属性的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumCustomAttributes( 
   IEnumDebugCustomAttributes** ppEnum
);
```

```csharp
int EnumCustomAttributes(
   out IEnumDebugCustomAttributes ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回表示自定义属性列表的 [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) 对象;否则，如果没有自定义特性，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或 S_FALSE 如果此字段没有自定义特性，则为。 否则，将返回错误代码;

## <a name="remarks"></a>备注
 一个字段可以具有多个自定义属性。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
