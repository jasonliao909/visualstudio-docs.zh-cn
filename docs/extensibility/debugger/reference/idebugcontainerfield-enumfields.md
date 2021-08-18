---
description: 为容器的字段创建枚举器。
title: IDebugContainerField：：EnumFields |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugContainerField::EnumFields
helpviewer_keywords:
- IDebugContainerField::EnumFields method
ms.assetid: 9e5e681b-ad49-4c62-bd95-4afa11d61a57
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 582521a59cc4652aaf3bdf92f5f0c24b19283e20
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103658"
---
# <a name="idebugcontainerfieldenumfields"></a>IDebugContainerField::EnumFields
为容器的字段创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumFields( 
   FIELD_KIND         dwKindFilter,
   FIELD_MODIFIERS    dwModifiersFilter,
   LPCOLESTR          pszNameFilter,
   NAME_MATCH         nameMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumFields(
   enum_ FIELD_KIND      dwKindFilter,
   enum_ FIELD_MODIFIERS dwModifiersFilter,
   string                pszNameFilter,
   NAME_MATCH            nameMatch,
   out IEnumDebugFields  ppEnum
);
```

## <a name="parameters"></a>参数
`dwKindFilter`\
[in]用于 [FIELD_KIND要](../../../extensibility/debugger/reference/field-kind.md) 枚举的字段的常量的组合。 字段类型可以描述存储类型（如类或基元）或特定信息，例如本地、参数或"this"指针。

`dwModifiersFilter`\
[in]用于 [FIELD_MODIFIERS要](../../../extensibility/debugger/reference/field-modifiers.md) 枚举的字段的常量的组合。 字段修饰符可以是访问权限（例如公共或专用）或存储信息（例如虚拟、静态或最终）。

`pszNameFilter`\
[in]要枚举的字段的名称。 如果要返回所有字段，则此值可以是 null 值。

`nameMatch`\
[in]一个来自 [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md) 值，该值控制搜索是否区分大小写。

`ppEnum`\
[out]返回表示 [字段列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有字段，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则S_OK或S_FALSE字段时返回 。 否则，返回错误代码。

## <a name="remarks"></a>备注
 例如，可以组合 、 和 参数，以选择名为 `dwKindFilter` `dwModifiersFilter` `pszNameFilter` "MyMethod"的所有公共虚拟方法。

## <a name="see-also"></a>请参阅
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [FIELD_KIND](../../../extensibility/debugger/reference/field-kind.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
