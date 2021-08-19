---
description: 指定要检索有关内存上下文的信息。
title: CONTEXT_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 36adf58598248bb6e59045e80b185dd2684b64b7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122120083"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
指定要检索有关内存上下文的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
typedef DWORD CONTEXT_INFO_FIELDS;
```

```csharp
public enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
```

## <a name="fields"></a>字段
`CIF_MODULEURL`\
初始化/使用 `bstrModuleUrl` 结构CONTEXT_INFO字段。 [](../../../extensibility/debugger/reference/context-info.md)

`CIF_FUNCTION`\
初始化/使用 `bstrFunction` 结构的 `CONTEXT_INFO` 字段。

`CIF_FUNCTIONOFFSET`\
初始化/使用 `posFunctionOffset` 结构的 `CONTEXT_INFO` 字段。

`CIF_ADDRESS`\
初始化/使用 `bstrAddress` 结构的 `CONTEXT_INFO` 字段。

`CIF_ADDRESSOFFSET`\
初始化/使用 `bstrAddressOffset` 结构的 `CONTEXT_INFO` 字段。

`CIF_ALLFIELDS`\
初始化/使用 结构的所有 `CONTEXT_INFO` 字段。

## <a name="remarks"></a>备注
这些值将参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)方法，以指示要初始化CONTEXT_INFO的字段[](../../../extensibility/debugger/reference/context-info.md)。

这些标志还用于指示结构的哪些字段在返回结构时 `CONTEXT_INFO` 有效。

这些值可以与位 OR 组合。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
