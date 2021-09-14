---
description: 该BUILT_TYPE结构指定有关从元数据获取的字段类型的信息。
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
ms.openlocfilehash: 3179ea403cd542a54d4b4a5e0a10776daa87b76f
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602488"
---
# <a name="built_type"></a>BUILT_TYPE
此结构指定有关从元数据获取的字段类型的信息。

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
符号来自的应用程序的 ID。 这用于唯一标识应用程序的实例。

`guidModule`\
包含此字段的模块的 GUID。

`pUnderlyingField`\
标识与此生成字段关联的基础字段的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象。

## <a name="remarks"></a>备注
当 结构的 字段设置为从 dwTYPE_KIND[](../../../extensibility/debugger/reference/type-info.md)枚举值 (时，此结构在 TYPE_INFO 结构中显示为联合的 `dwKind` `TYPE_INFO` `TYPE_KIND_BUILT` 一) 。 [](../../../extensibility/debugger/reference/dwtype-kind.md)

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
