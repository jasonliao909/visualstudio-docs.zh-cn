---
description: 获取DEBUG_PROPERTY_INFO属性的属性结构。
title: IDebugProperty2：：GetPropertyInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetPropertyInfo
helpviewer_keywords:
- IDebugProperty2::GetPropertyInfo
ms.assetid: 39d6e942-df72-4c84-a5d9-a386d112714c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 26ffe65e84f8c878644e3fd4cec7fa3ad16ba544c221c8a02779870253d923df
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338704"
---
# <a name="idebugproperty2getpropertyinfo"></a>IDebugProperty2::GetPropertyInfo
获取 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 属性的属性结构。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPropertyInfo ( 
   DEBUGPROP_INFO_FLAGS dwFields,
   DWORD                nRadix,
   DWORD                dwTimeout,
   IDebugReference2**   rgpArgs,
   DWORD                dwArgCount,
   DEBUG_PROPERTY_INFO* pPropertyInfo
);
```

```cpp
int GetPropertyInfo ( 
   enum_DEBUGPROP_INFO_FLAGS dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_PROPERTY_INFO[]     pPropertyInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]集合中的值 [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) 枚举，用于指定在 结构中填充哪些 `pPropertyInfo` 字段。

`nRadix`\
[in]用于设置任何数值信息格式的基数。

`dwTimeout`\
[in]指定在从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`rgpArgs`\
[in， out]保留供将来使用;设置为 null 值。

`dwArgCount`\
[in]保留供将来使用;设置为零。

`pPropertyInfo`\
[out]一 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 属性说明填充的一个结构。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
