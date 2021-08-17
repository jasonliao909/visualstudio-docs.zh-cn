---
description: 描述不同类型的地址。
title: DEBUG_ADDRESS_UNION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab8f7b268f347380284662b2ef35dab03e99513f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122073118"
---
# <a name="debug_address_union"></a>DEBUG_ADDRESS_UNION
描述不同类型的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagDEBUG_ADDRESS_UNION {
   ADDRESS_KIND dwKind;
   union {
      NATIVE_ADDRESS                  addrNative;
      UNMANAGED_ADDRESS_THIS_RELATIVE addrThisRel;
      UNMANAGED_ADDRESS_PHYSICAL      addrUPhysical;
      METADATA_ADDRESS_METHOD         addrMethod;
      METADATA_ADDRESS_FIELD          addrField;
      METADATA_ADDRESS_LOCAL          addrLocal;
      METADATA_ADDRESS_PARAM          addrParam;
      METADATA_ADDRESS_ARRAYELEM      addrArrayElem;
      METADATA_ADDRESS_RETVAL         addrRetVal;
      DWORD                           unused;
   } addr;
} DEBUG_ADDRESS_UNION;
```

```csharp
public struct DEBUG_ADDRESS_UNION {
   public ADDRESS_KIND dwKind;
   public IntPtr       unionmember;
}
```

## <a name="members"></a>成员
`dwKind`\
一 [个来自](../../../extensibility/debugger/reference/address-kind.md) ADDRESS_KIND 枚举的值，指定如何解释联合。

`addr.addrNative`\
[仅 C++]如果 = [NATIVE_ADDRESS，](../../../extensibility/debugger/reference/native-address.md) `dwKind` 包含ADDRESS_KIND_NATIVE。

`addr.addrThisRel`\
[仅 C++]如果 =[UNMANAGED_ADDRESS_THIS_RELATIVE，](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) 包含 `dwKind` ADDRESS_KIND_UNMANAGED_THIS_RELATIVE。

`addr.addUPhysical`\
[仅 C++]如果 =[UNMANAGED_ADDRESS_PHYSICAL，](../../../extensibility/debugger/reference/unmanaged-address-physical.md) `dwKind` 包含ADDRESS_KIND_UNMANAGED_PHYSICAL。

`addr.addrMethod`\
[仅 C++]如果 =[METADATA_ADDRESS_METHOD，](../../../extensibility/debugger/reference/metadata-address-method.md) `dwKind` 包含ADDRESS_KIND_METHOD。

`addr.addrField`\
[仅 C++]如果 =[METADATA_ADDRESS_FIELD，](../../../extensibility/debugger/reference/metadata-address-field.md) `dwKind` 包含ADDRESS_KIND_FIELD。

`addr.addrLocal`\
[仅 C++]如果 =[METADATA_ADDRESS_LOCAL，](../../../extensibility/debugger/reference/metadata-address-local.md) 包含 `dwKind` ADDRESS_KIND_LOCAL。

`addr.addrParam`\
[仅 C++]如果 =[METADATA_ADDRESS_PARAM，](../../../extensibility/debugger/reference/metadata-address-param.md) 包含 `dwKind` ADDRESS_KIND_PARAM。

`addr.addrArrayElem`\
[仅 C++]如果 =[METADATA_ADDRESS_ARRAYELEM，](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) `dwKind` 包含ADDRESS_KIND_ARRAYELEM。

`addr.addrRetVal`\
[仅 C++]如果 =[METADATA_ADDRESS_RETVAL，](../../../extensibility/debugger/reference/metadata-address-retval.md) 包含 `dwKind` ADDRESS_KIND_RETVAL。

`addr.unused`\
[仅 C++] 填充。

`addr`\
[仅 C++]联合的名称。

`unionmember`\
[仅 C# ]需要基于 将此值封送到适当的结构类型 `dwKind` 。 有关联合和解释之间的 `dwKind` 关联，请参阅备注。

## <a name="remarks"></a>备注
此结构是 DEBUG_ADDRESS[](../../../extensibility/debugger/reference/debug-address.md)结构的一部分，表示许多不同类型的地址之一 (通过调用 `DEBUG_ADDRESS` [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)方法来填充) 。

 [仅 C# ]下表显示了如何解释 `unionmember` 每类地址的成员。 该示例演示了如何为一种地址完成此操作。

|`dwKind`|`unionmember` 解释为|
|--------------|----------------------------------|
|`ADDRESS_KIND_NATIVE`|[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)|
|`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`|[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)|
|`ADDRESS_KIND_UNMANAGED_PHYSICAL`|[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)|
|`ADDRESS_KIND_METHOD`|[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)|
|`ADDRESS_KIND_FIELD`|[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)|
|`ADDRESS_KIND_LOCAL`|[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)|
|`ADDRESS_KIND_PARAM`|[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)|
|`ADDRESS_KIND_ARRAYELEM`|[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)|
|`ADDRESS_KIND_RETVAL`|[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)|

## <a name="example"></a>示例
此示例演示如何在 C# 中解释 () `METADATA_ADDRESS_ARRAYELEM` 类型的 `DEBUG_ADDRESS_UNION` 地址类型。 其余元素的解释方式完全相同。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(DEBUG_ADDRESS_UNION dau)
        {
            if (dau.dwKind == (uint)enum_ADDRESS_KIND.ADDRESS_KIND_METADATA_ARRAYELEM)
            {
                 METADATA_ADDRESS_ARRAYELEM arrayElem =
                     (METADATA_ADDRESS_ARRAYELEM)Marshal.PtrToStructure(dau.unionmember,
                                 typeof(METADATA_ADDRESS_ARRAYELEM));
            }
        }
    }
}
```

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
- [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
