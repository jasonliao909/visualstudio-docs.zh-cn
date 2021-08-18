---
description: 将此属性的值设置为给定引用的值。
title: IDebugProperty2：： SetValueAsReference |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e515a70a90440eae1277688aab2b98df8ced787b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110977"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
将此属性的值设置为给定引用的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValueAsReference(
   IDebugReference2** rgpArgs,
   DWORD              dwArgCount,
   IDebugReference2*  pValue,
   DWORD              dwTimeout
);
```

```csharp
int SetValueAsReference(
   IDebugReference2[] rgpArgs,
   uint               dwArgCount,
   IDebugReference2   pValue,
   uint               dwTimeout
);
```

## <a name="parameters"></a>参数
`rgpArgs`\
中要传递给托管代码属性 setter 的参数数组。 如果属性资源库不采用参数，或此 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象不引用此类属性资源库，则 `rgpArgs` 应为 null 值。 此参数通常为 null 值。

`dwArgCount`\
中数组中的参数数量 `rgpArgs` 。

`pValue`\
中 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象形式的引用，它指向用于设置此属性的值。

`dwTimeout`\
中设置值所需的时间（以毫秒为单位）。 典型值为 `INFINITE` 。 这会影响任何可能的评估所需的时间长度。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码，通常为以下值之一：

|错误|说明|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|不支持从引用设置值。|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法设置值，因为此属性引用方法。|
|`E_SETVALUE_VALUE_IS_READONLY`|该值为只读，不能设置。|
|`E_NOTIMPL`|该方法未实现。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
