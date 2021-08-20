---
description: 指定调试模块信息的标志。
title: MODULE_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c3e75ec051787cfb08754e459012e4df3556e113
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110756"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
指定调试模块信息的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>字段
 `MIF_NONE`\
 初始化/使用 结构中没有任何字段。

 `MIF_NAME`\
 初始化/使用 `m_bstrName` 结构MODULE_INFO字段。 [](../../../extensibility/debugger/reference/module-info.md)

 `MIF_URL`\
 初始化/使用 `m_bstrUrl` 结构中的 `MODULE_INFO` 字段。

 `MIF_VERSION`\
 初始化/使用 `m_bstrVersion` 结构中的 `MODULE_INFO` 字段。

 `MIF_DEBUGMESSAGE`\
 初始化/使用 `m_bstrDebugMessage` 结构中的 `MODULE_INFO` 字段。

 `MIF_LOADADDRESS`\
 初始化/使用 `m_addrLoadAddress` 结构中的 `MODULE_INFO` 字段。

 `MIF_PREFFEREDADDRESS`\
 初始化/使用 `m_addrPreferredLoadAddress` 结构中的 `MODULE_INFO` 字段。

 `MIF_SIZE`\
 初始化/使用 `m_dwSize` 结构中的 `MODULE_INFO` 字段。

 `MIF_LOADORDER`\
 初始化/使用 `m_dwLoadOrder` 结构中的 `MODULE_INFO` 字段。

 `MIF_TIMESTAMP`\
 初始化/使用 `m_TimeStamp` 结构中的 `MODULE_INFO` 字段。

 `MIF_URLSYMBOLLOCATION`\
 初始化/使用 `m_bstrUrlSymbolLocation` 结构中的 `MODULE_INFO` 字段。

 `MIF_FLAGS`\
 初始化/使用 `m_dwModuleFlags` 结构中的 `MODULE_INFO` 字段。

 `MIF_ALLFIELDS`\
 初始化/使用 结构中的所有 `MODULE_INFO` 字段。

## <a name="remarks"></a>备注
 这些值作为参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)方法，以指示要初始化MODULE_INFO的字段。 [](../../../extensibility/debugger/reference/module-info.md)

 这些值还用于 结构 `MODULE_INFO` ，以指示哪些字段已使用且有效。

 这些标志可以与位 合并 `OR` 。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
