---
description: 此结构指定有关字段类型的各种信息。
title: TYPE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0a9c4381492e2909ab79b58ac0e9024bb7237f2a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602379"
---
# <a name="type_info"></a>TYPE_INFO
此结构指定有关字段类型的各种信息。

## <a name="syntax"></a>语法

```cpp
struct _tagTYPE_INFO_UNION {
   dwTYPE_KIND dwKind;
   union {
      METADATA_TYPE typeMeta;
      PDB_TYPE      typePdb;
      BUILT_TYPE    typeBuilt;
      DWORD         unused;
   } type;
} TYPE_INFO;
```

```csharp
public struct TYPE_INFO {
   public uint   dwKind;
   public IntPtr unionmember;
};
```

## <a name="members"></a>成员
 `dwKind`\
 一个来自 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 值，该值确定如何解释联合。

 `type.typeMeta`\
 [仅 C++]如果 为 [METADATA_TYPE，](../../../extensibility/debugger/reference/metadata-type.md) 则包含 `dwKind` 一个结构 `TYPE_KIND_METADATA` 。

 `type.typePdb`\
 [仅 C++]如果 为 [PDB_TYPE，](../../../extensibility/debugger/reference/pdb-type.md) 则包含 `dwKind` 一个结构 `TYPE_KIND_PDB` 。

 `type.typeBuilt`\
 [仅 C++]如果 为 [BUILT_TYPE，](../../../extensibility/debugger/reference/built-type.md) 则包含 `dwKind` 一个结构 `TYPE_KIND_BUILT` 。

 `type.unused`\
 未使用的填充。

 `type`\
 联合的名称。

 `unionmember`\
 [仅 C# ]基于 将此方法封送到适当的结构类型 `dwKind` 。

## <a name="remarks"></a>备注
 此结构将传递给 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) 方法，该方法用于填充它。 如何解释结构的内容取决于 `dwKind` 字段。

> [!NOTE]
> [仅 C++]如果 等于 ，则销毁结构时需要释放基础 `dwKind` `TYPE_KIND_BUILT` [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) `TYPE_INFO` 对象。 可以通过调用 `typeInfo.type.typeBuilt.pUnderlyingField->Release()` 来完成此操作。

 [仅 C# ]下表显示了如何解释 `unionmember` 每种类型的成员。 该示例演示了如何针对某种类型完成此操作。

|`dwKind`|`unionmember` 解释为|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>示例
 此示例演示如何在 `unionmember` C# 中解释 `TYPE_INFO` 结构的成员。 此示例演示仅解释一个类型 () `TYPE_KIND_METADATA` 但其他类型解释方式完全相同。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(TYPE_INFO ti)
        {
            if (ti.dwKind == (uint)enum_dwTypeKind.TYPE_KIND_METADATA)
            {
                 METADATA_TYPE dataType = (METADATA_TYPE)Marshal.PtrToStructure(ti.unionmember,
                                               typeof(METADATA_TYPE));
            }
        }
    }
}
```

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
