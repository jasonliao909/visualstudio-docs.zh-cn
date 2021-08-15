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
ms.openlocfilehash: abdd04428695e105b7e9f3e14e740beef3a347574171296768af9a9637eaa592
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415267"
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
 初始化/不使用结构中的任何字段。

 `MIF_NAME`\
 初始化/使用 `m_bstrName` [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 结构中的字段。

 `MIF_URL`\
 初始化/使用 `m_bstrUrl` 结构中的字段 `MODULE_INFO` 。

 `MIF_VERSION`\
 初始化/使用 `m_bstrVersion` 结构中的字段 `MODULE_INFO` 。

 `MIF_DEBUGMESSAGE`\
 初始化/使用 `m_bstrDebugMessage` 结构中的字段 `MODULE_INFO` 。

 `MIF_LOADADDRESS`\
 初始化/使用 `m_addrLoadAddress` 结构中的字段 `MODULE_INFO` 。

 `MIF_PREFFEREDADDRESS`\
 初始化/使用 `m_addrPreferredLoadAddress` 结构中的字段 `MODULE_INFO` 。

 `MIF_SIZE`\
 初始化/使用 `m_dwSize` 结构中的字段 `MODULE_INFO` 。

 `MIF_LOADORDER`\
 初始化/使用 `m_dwLoadOrder` 结构中的字段 `MODULE_INFO` 。

 `MIF_TIMESTAMP`\
 初始化/使用 `m_TimeStamp` 结构中的字段 `MODULE_INFO` 。

 `MIF_URLSYMBOLLOCATION`\
 初始化/使用 `m_bstrUrlSymbolLocation` 结构中的字段 `MODULE_INFO` 。

 `MIF_FLAGS`\
 初始化/使用 `m_dwModuleFlags` 结构中的字段 `MODULE_INFO` 。

 `MIF_ALLFIELDS`\
 初始化/使用结构中的所有字段 `MODULE_INFO` 。

## <a name="remarks"></a>备注
 这些值作为参数传递给 [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) 方法，以指示要初始化 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 结构的哪些字段。

 这些值还在结构中用于 `MODULE_INFO` 指示哪些字段已使用并且有效。

 这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
