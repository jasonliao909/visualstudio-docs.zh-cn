---
description: BUILT_TYPE 结构指定了来自元数据的字段类型的相关信息。
title: BUILT_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 81b18a6e238b71a7c91445b551beb34dd081e53c24b5301cd58c495a04e1e733
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360958"
---
# <a name="built_type"></a>BUILT_TYPE
此结构指定了来自元数据的字段类型的相关信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_BUILT {
    ULONG32      ulAppDomainID;
    GUID         guidModule;
    IDebugField* pUnderlyingField;
} BUILT_TYPE;
```

```csharp
public struct BUILT_TYPE {
    public uint        ulAppDomainID;
    public Guid        guidModule;
    public IDebugField pUnderlyingField;
};
```

## <a name="members"></a>成员
`ulAppDomainID`\
符号所源自的应用程序的 ID。 用于唯一标识应用程序的实例。

`guidModule`\
包含此字段的模块的 GUID。

`pUnderlyingField`\
一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，该对象标识与此生成字段关联的基础字段。

## <a name="remarks"></a>备注
当结构的[](../../../extensibility/debugger/reference/type-info.md) `dwKind` 字段 `TYPE_INFO` 设置为 `TYPE_KIND_BUILT` 从[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举) 中的值 (时，此结构显示为 TYPE_INFO 结构中联合的一部分。

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
