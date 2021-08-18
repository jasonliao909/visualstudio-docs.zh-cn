---
description: 指定要检索的有关断点的成功解决方法的信息。
title: BPRESI_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPRESI_FIELDS
helpviewer_keywords:
- BPRESI_FIELDS enumeration
ms.assetid: 99f17b1e-3e67-4f85-89d6-5c6cf45c8008
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d47be3c63724b18b92fac9d253878b25c72c68dc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122120213"
---
# <a name="bpresi_fields"></a>BPRESI_FIELDS
指定要检索的有关断点的成功解决方法的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_BPRESI_FIELDS {
    BPRESI_BPRESLOCATION = 0x0001,
    BPRESI_PROGRAM       = 0x0002,
    BPRESI_THREAD        = 0x0004,
    BPRESI_ALLFIELDS     = 0xffffffff
};
typedef DWORD BPRESI_FIELDS;
```

```csharp
public enum enum_BPRESI_FIELDS {
    BPRESI_BPRESLOCATION = 0x0001,
    BPRESI_PROGRAM       = 0x0002,
    BPRESI_THREAD        = 0x0004,
    BPRESI_ALLFIELDS     = 0xffffffff
};
```

## <a name="fields"></a>字段
`BPRESI_BPRESLOCATION`\
初始化/使用 `bpResLocation` [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 结构的 (断点解析位置) "字段。

`BPRESI_PROGRAM`\
初始化/使用 `pProgram` 结构的字段 `BP_RESOLUTION_INFO` 。

`BPRESI_THREAD`\
初始化/使用 `pThread` 结构的字段 `BP_RESOLUTION_INFO` 。

`BPRESI_ALLFIELDS`\
指定所有字段。

## <a name="remarks"></a>备注
传递给 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md) 方法以指示要初始化 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) 结构的哪些字段。

这些标志还用于指示在 `BP_RESOLUTION_INFO` 返回结构时使用的结构字段和有效字段。

这些值可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)
