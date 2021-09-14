---
description: 此结构表示方法或函数的返回值。
title: METADATA_ADDRESS_RETVAL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a95ac1b17cfec2a2b78b74233ad5f4c5addafdd0
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665392"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
此结构表示方法或函数的返回值。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_RETVAL {
   _mdToken tokMethod;
   DWORD    dwCorType;
   DWORD    dwSigSize;
   BYTE     rgSig[10];
} METADATA_ADDRESS_RETVAL;
```

```csharp
public struct METADATA_ADDRESS_RETVAL {
   public int    tokMethod;
   public uint   dwCorType;
   public uint   dwSigSize;
   public byte[] rgSig;
}
```

## <a name="members"></a>成员
 `tokMethod`\
 此返回值所针对的方法的 ID。

 `dwCorType`\
 返回值的基类型。 这是从 .NET Framework `CorElementType` SDK corhdr.h 文件中定义的 枚举中的值。

 `dwSigSize`\
 返回值签名的大小 (存储在 `rgSig`) 。

 `rgSig`\
 构成返回值的签名的字节数组。

## <a name="remarks"></a>备注
 当 结构的 字段[设置为](../../../extensibility/debugger/reference/debug-address-union.md)从 DEBUG_ADDRESS_UNION 枚举集合中 (值时，此结构是 ADDRESS_KIND 中的联合 `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_RETVAL`) 。 [](../../../extensibility/debugger/reference/address-kind.md)

## <a name="requirements"></a>要求
 标头：sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
