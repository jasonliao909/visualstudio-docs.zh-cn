---
description: 指定要检索有关断点失败解析的信息。
title: BPERESI_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: effaa705459b0009e9462898109c951df9cc4436dbee5c59222f703f04cc2b49
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390388"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
指定要检索有关断点失败解析的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
typedef DWORD BPERESI_FIELDS;
```

```csharp
public enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>字段
`PERESI_BPRESLOCATION`\
初始化/使用 (`bpResLocation` 结构) 断点BP_ERROR_RESOLUTION_INFO位置[](../../../extensibility/debugger/reference/bp-error-resolution-info.md)。

`BPERESI_PROGRAM`\
初始化/使用 `pProgram` 结构的 `BP_ERROR_RESOLUTION_INFO` 字段。

`BPERESI_THREAD`\
初始化/使用 `pThread` 结构的 `BP_ERROR_RESOLUTION_INFO` 字段。

`BPERESI_MESSAGE`\
初始化/使用 `bstrMessage` 结构的 `BP_ERROR_RESOLUTION_INFO` 字段。

`BPERESI_TYPE`\
初始化/使用 (`dwType` 结构) 字段的断 `BP_ERROR_RESOLUTION_INFO` 点类型。

`BPERESI_ALLFIELDS`\
初始化/使用 结构的所有 `BP_ERROR_RESOLUTION_INFO` 字段。

## <a name="remarks"></a>备注
作为参数传递给[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)方法，以指示要初始化BP_ERROR_RESOLUTION_INFO的[](../../../extensibility/debugger/reference/bp-error-resolution-info.md)字段。

这些值还用于指示结构中使用哪些字段，在返回该结构 `BP_ERROR_RESOLUTION_INFO` 时有效。

这些值可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
