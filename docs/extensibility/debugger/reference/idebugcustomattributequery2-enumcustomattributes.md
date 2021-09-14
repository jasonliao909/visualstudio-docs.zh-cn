---
description: 获取附加到此字段的所有自定义属性的枚举器。
title: IDebugCustomAttributeQuery2：：EnumCustomAttributes |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3569887190c36c2dd4d614aa8949914f6ae275d2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664536"
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

## <a name="parameters"></a>parameters
`ppEnum`\
[out]返回表示 [自定义属性列表的 IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) 对象;否则，如果没有自定义属性，则 返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则S_OK此字段S_FALSE自定义属性时返回属性或属性。 否则， 将返回错误代码;

## <a name="remarks"></a>备注
 一个字段可以有多个自定义属性。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
