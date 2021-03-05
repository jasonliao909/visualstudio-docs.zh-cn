---
description: 给定类型参数的数组，构造一个字段实例。
title: IDebugGenericFieldDefinition：： ConstructInstantiation |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- ConstructInstantiation
- IDebugGenericFieldDefinition::ConstructInstantiation
ms.assetid: ef8ae261-a98b-4dc2-93b3-7c5191818ba2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8b43bf1ccc232c0b378a6e3bd3d788519e456da9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165483"
---
# <a name="idebuggenericfielddefinitionconstructinstantiation"></a>IDebugGenericFieldDefinition::ConstructInstantiation
给定类型参数的数组，构造一个字段实例。

## <a name="syntax"></a>语法

```cpp
HRESULT ConstructInstantiation(
   ULONG32       cArgs,
   IDebugField** ppArgs,
   IDebugField** ppConstructedField
);
```

```csharp
int ConstructInstantiation(
   uint            cArgs,
   IDebugField[]   ppArgs,
   out IDebugField ppConstructedField
);
```

## <a name="parameters"></a>参数
`cArgs`\
中数组中的参数数量 `ppArgs` 。

`ppArgs`\
中包含类型参数的数组。 类型实参必须是 (非泛型或完全实例化的泛型) 的封闭类型。

`ppConstructedField`\
弄返回表示新字段的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 不检查约束。

## <a name="see-also"></a>另请参阅
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
