---
description: 指定地址类型。
title: ADDRESS_KIND |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ADDRESS_KIND
helpviewer_keywords:
- ADDRESS_KIND enumeration
ms.assetid: 3a12fbec-7088-4cf9-8f6f-ad8ddec6009a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77bc222e5d884fcbc464734654eca1e1535c6f0f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122030407"
---
# <a name="address_kind"></a>ADDRESS_KIND
指定地址类型。

## <a name="syntax"></a>语法

```cpp
enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
typedef DWORD ADDRESS_KIND;
```

```csharp
public enum enum_ADDRESS_KIND {
    ADDRESS_KIND_NATIVE                  = 0x0001,
    ADDRESS_KIND_UNMANAGED_THIS_RELATIVE = 0x0002,
    ADDRESS_KIND_UNMANAGED_PHYSICAL      = 0x0005,
    ADDRESS_KIND_METADATA_METHOD         = 0x0010,
    ADDRESS_KIND_METADATA_FIELD          = 0x0011,
    ADDRESS_KIND_METADATA_LOCAL          = 0x0012,
    ADDRESS_KIND_METADATA_PARAM          = 0x0013,
    ADDRESS_KIND_METADATA_ARRAYELEM      = 0x0014,
    ADDRESS_KIND_METADATA_RETVAL         = 0x0015,
};
```

## <a name="fields"></a>字段
`ADDRESS_KIND_NATIVE`\
本机地址，由[NATIVE_ADDRESS表示。](../../../extensibility/debugger/reference/native-address.md)

`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`\
一个非托管地址，相对于 (`this` `Me` 指针Visual Basic) ，由[](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)UNMANAGED_ADDRESS_THIS_RELATIVE 表示。

`ADDRESS_KIND_UNMANAGED_PHYSICAL`\
非托管物理地址，由 UNMANAGED_ADDRESS_PHYSICAL[表示。](../../../extensibility/debugger/reference/unmanaged-address-physical.md)

`ADDRESS_KIND_METHOD`\
类的一个方法，由 METADATA_ADDRESS_METHOD[表示。](../../../extensibility/debugger/reference/metadata-address-method.md)

`ADDRESS_KIND_FIELD`\
类的一个字段，由[METADATA_ADDRESS_FIELD表示。](../../../extensibility/debugger/reference/metadata-address-field.md)

`ADDRESS_KIND_LOCAL`\
地址用于局部变量，由[METADATA_ADDRESS_LOCAL表示。](../../../extensibility/debugger/reference/metadata-address-local.md)

`ADDRESS_KIND_PARAM`\
方法或函数参数，由[METADATA_ADDRESS_PARAM表示。](../../../extensibility/debugger/reference/metadata-address-param.md)

`ADDRESS_KIND_ARRAYELEM`\
一个数组元素，由 METADATA_ADDRESS_ARRAYELEM[表示。](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)

`ADDRESS_KIND_RETVAL`\
一个返回值，由[METADATA_ADDRESS_RETVAL表示。](../../../extensibility/debugger/reference/metadata-address-retval.md)

## <a name="remarks"></a>备注
[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)方法返回DEBUG_ADDRESS，该结构包含可能的结构（即[DEBUG_ADDRESS_UNION联合）。](../../../extensibility/debugger/reference/debug-address-union.md) [](../../../extensibility/debugger/reference/debug-address.md) `dwKind`结构的 字段 `DEBUG_ADDRESS_UNION` 保存 `ADDRESS_KIND` 值，并描述如何解释联合字段。

## <a name="requirements"></a>要求
标头：sh.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
