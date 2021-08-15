---
description: 检索属性的子项的列表。
title: IDebugProperty2：：EnumChildren |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::EnumChildren
helpviewer_keywords:
- IDebugProperty2::EnumChildren
ms.assetid: cf79f666-65d1-417c-af7c-9271bac9a267
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89a377ea09822db6ac86ddd19c714021099df995733fcb1bd2e43fd0a1df4ec1
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449061"
---
# <a name="idebugproperty2enumchildren"></a>IDebugProperty2::EnumChildren
检索属性的子项的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumChildren ( 
   DEBUGPROP_INFO_FLAGS      dwFields,
   DWORD                     dwRadix,
   REFGUID                   guidFilter,
   DBG_ATTRIB_FLAGS          dwAttribFilter,
   LPCOLESTR                 pszNameFilter,
   DWORD                     dwTimeout,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFields,
   uint                        dwRadix,
   ref Guid                    guidFilter,
   uint                        dwAttribFilter,
   string                      pszNameFilter,
   uint                        dwTimeout,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]来自枚举[DEBUGPROP_INFO_FLAGS标志的组合](../../../extensibility/debugger/reference/debugprop-info-flags.md)，指定要填充枚举DEBUG_PROPERTY_INFO结构中的哪些字段。 [](../../../extensibility/debugger/reference/debug-property-info.md)

`dwRadix`\
[in]指定用于设置任何数值信息格式的基数。

`guidFilter`\
[in]与 和 参数一起用于选择要枚举的 `dwAttribFilter` `pszNameFilter` `DEBUG_PROPERTY_INFO` 子项的筛选器的 GUID。 例如， `guidFilterLocals` 筛选局部变量。

`dwAttribFilter`\
[in]来自 DBG_ATTRIB_FLAGS [标志的组合](../../../extensibility/debugger/reference/dbg-attrib-flags.md) ，指定要枚举的对象类型，例如，对于可能为此属性的子 `DBG_ATTRIB_METHOD` 对象的所有方法。 与 和 参数 `guidFilter` `pszNameFilter` 结合使用。

`pszNameFilter`\
[in]与 和 参数一起用于 `guidFilter` 选择要枚举的 `dwAttribFilter` `DEBUG_PROPERTY_INFO` 子项的筛选器的名称。 例如，将此参数设置为"MyX"会筛选所有名称为"MyX"的子项目。

`dwTimeout`\
[in]指定在从此方法返回之前等待的最大时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

`ppEnum`\
[out]返回包含 [子属性列表的 IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
