---
title: IDebugGenericFieldDefinition：： TypeParamCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- TypeParamCount
- IDebugGenericFieldDefinition::TypeParamCount
ms.assetid: d41dd5ea-aa25-4bf3-bcfd-e0bf451ead49
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d006e55d9ca00ff828c59beb698441807f70c6e3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903216"
---
# <a name="idebuggenericfielddefinitiontypeparamcount"></a>IDebugGenericFieldDefinition::TypeParamCount
检索与泛型字段关联的类型参数的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT TypeParamCount(
   ULONG32* pcParams
);
```

```csharp
int TypeParamCount(
   ref uint pcParams
);
```

## <a name="parameters"></a>parameters
`pcParams`\
[in，out]类型参数的数目。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 如果为 List \<T> ，则此方法返回 1; 如果为 list \<T1,T2> ，则此方法返回2。 如果没有类型参数，则此方法返回0。

## <a name="see-also"></a>另请参阅
- [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
