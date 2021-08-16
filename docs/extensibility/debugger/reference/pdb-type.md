---
description: 此结构指定有关从 PDB 符号获取的字段类型的信息。
title: PDB_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PDB_TYPE
helpviewer_keywords:
- PDB_TYPE structure
ms.assetid: 1c1bb772-77d6-4870-90b2-fd9247d0004e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3b2a812fa59c8017b6a4296d0172fc2225d099470685450c50e2c618b6bd66f4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415164"
---
# <a name="pdb_type"></a>PDB_TYPE

此结构指定有关从 PDB 符号获取的字段类型的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_PDB {
    ULONG32 ulAppDomainID;
    GUID    guidModule;
    DWORD   symid;
} PDB_TYPE;
```

```csharp
public struct PDB_TYPE {
    public uint ulAppDomainID;
    public Guid guidModule;
    public uint symid;
};
```

## <a name="members"></a>成员

`ulAppDomainID`\
符号来自的应用程序的 ID。 这用于唯一标识应用程序的实例。

`guidModule`\
包含此字段的模块的 GUID。

`symid`\
与此字段对应的符号的 ID。

## <a name="remarks"></a>备注

当 结构的 字段[设置为](../../../extensibility/debugger/reference/type-info.md)从 dwTYPE_KIND 枚举值 (时，此结构在 TYPE_INFO 结构中显示为联合的 `dwKind` `TYPE_INFO` `TYPE_KIND_PDB` 一) 。 [](../../../extensibility/debugger/reference/dwtype-kind.md)

## <a name="requirements"></a>要求

标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
