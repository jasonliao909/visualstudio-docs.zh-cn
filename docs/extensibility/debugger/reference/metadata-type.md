---
description: METADATA_TYPE 结构指定了来自元数据的字段类型的相关信息。
title: METADATA_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5a76e051e146985338564d497323b6232b35a4a1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079847"
---
# <a name="metadata_type"></a>METADATA_TYPE
此结构指定了来自元数据的字段类型的相关信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_METADATA {
   ULONG32  ulAppDomainID;
   GUID     guidModule;
   _mdToken tokClass;
} METADATA_TYPE;
```

```csharp
public struct METADATA_TYPE {
   public uint ulAppDomainID;
   public Guid guidModule;
   public int  tokClass;
};
```

## <a name="parameters"></a>参数
 `ulAppDomainID`\
 符号所源自的应用程序的 ID。 用于唯一标识应用程序的实例。

 `guidModule`\
 包含此字段的模块的 GUID。

 `tokClass`\
 此类型的元数据标记 ID。

 [C + +] `_mdToken` 是 `typedef` 32 位的 `int` 。

## <a name="remarks"></a>备注
 当结构的[](../../../extensibility/debugger/reference/type-info.md) `dwKind` 字段 `TYPE_INFO` 设置为 `TYPE_KIND_METADATA` 从[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举) 中的值 (时，此结构显示为 TYPE_INFO 结构中联合的一部分。

 `tokClass`该值是唯一标识某个类型的元数据标记。 有关如何解释元数据标记 ID 的上限的详细信息，请参阅 `CorTokenType` .NET FRAMEWORK SDK 中 corhdr.h 文件中的枚举。

## <a name="requirements"></a>要求
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
