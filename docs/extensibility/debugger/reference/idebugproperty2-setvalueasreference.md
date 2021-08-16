---
description: 将此属性的值设置为给定引用的值。
title: IDebugProperty2：：SetValueAsReference |Microsoft Docs
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
ms.openlocfilehash: 3bd14716be1edaf691aca31212fd9c5b1bad86547b1a877dc28bd0360089ff04
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449022"
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
[in]要传递给托管代码属性资源库的参数数组。 如果属性 setter 不接受参数，或者此 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象未引用此类属性 setter，则 `rgpArgs` 应为 null 值。 此参数通常为 null 值。

`dwArgCount`\
[in]数组中的参数 `rgpArgs` 数。

`pValue`\
[in]对要用于设置此属性的值的引用（采用 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 对象的形式）。

`dwTimeout`\
[in]设置值需要的时间（以毫秒为单位）。 典型值为 `INFINITE` 。 这会影响任何可能的评估可能需要的时间长度。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码，通常为下列代码之一：

|错误|说明|
|-----------|-----------------|
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|不支持从引用设置值。|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法设置值，因为此属性引用方法。|
|`E_SETVALUE_VALUE_IS_READONLY`|该值是只读的，无法设置。|
|`E_NOTIMPL`|该方法未实现。|

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
