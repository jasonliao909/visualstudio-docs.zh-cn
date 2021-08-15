---
description: 描述 DLL、EXE (程序集的特定模块) 。
title: MODULE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO
helpviewer_keywords:
- MODULE_INFO structure
ms.assetid: f2e06180-1ab3-4eb5-a428-7994cceb61b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3ed9dd2e86c04771b8bb3b6c5fa87279d7bb41738b959b22ce51ce487029851c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338236"
---
# <a name="module_info"></a>MODULE_INFO
描述 DLL、EXE (程序集的特定模块) 。

## <a name="syntax"></a>语法

```cpp
typedef struct tagMODULE_INFO { 
   MODULE_INFO_FIELDS dwValidFields;
   BSTR               m_bstrName;
   BSTR               m_bstrUrl;
   BSTR               m_bstrVersion;
   BSTR               m_bstrDebugMessage;
   UINT64             m_addrLoadAddress;
   UINT64             m_addrPreferredLoadAddress;
   DWORD              m_dwSize;
   DWORD              m_dwLoadOrder;
   FILETIME           m_TimeStamp;
   BSTR               m_bstrUrlSymbolLocation;
   MODULE_FLAGS       m_dwModuleFlags;
} MODULE_INFO;
```

```csharp
public struct MODULE_INFO { 
   public uint     dwValidFields;
   public string   m_bstrName;
   public string   m_bstrUrl;
   public string   m_bstrVersion;
   public string   m_bstrDebugMessage;
   public ulong    m_addrLoadAddress;
   public ulong    m_addrPreferredLoadAddress;
   public uint     m_dwSize;
   public uint     m_dwLoadOrder;
   public FILETIME m_TimeStamp;
   public string   m_bstrUrlSymbolLocation;
   public uint     m_dwModuleFlags;
};
```

## <a name="members"></a>成员
 `dwValidFields`\
 集合中标志的组合 [MODULE_INFO_FIELDS，](../../../extensibility/debugger/reference/module-info-fields.md) 用于指定要填充哪些字段。

 `m_bstrName`\
 模块名。

 `m_bstrUrl`\
 模块 URL。

 `m_bstrVersion`\
 模块版本。

 `m_bstrDebugMessage`\
 有关模块的可选消息，例如"无法加载符号"。

 `m_addrLoadAddress`\
 模块加载地址。

 `m_addrPreferredLoadAddress`\
 模块的首选加载地址。

 `m_dwSize`\
 模块大小。

 `m_dwLoadOrder`\
 模块加载顺序。

 `m_TimeStamp`\
 上次修改符号文件的时间。

 `m_bstrUrlSymbolLocation`\
 符号文件的位置 (例如 \\ ""。) 模块中指定的参数。 用作查找模块符号的起始位置。

 `m_dwModuleFlags`\
 描述模块的MODULE_FLAGS集合中的[](../../../extensibility/debugger/reference/module-flags.md)标志组合。

## <a name="remarks"></a>备注
 此结构将传递到 [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md) 方法中填充它。

 此结构对应于"模块"窗口中列出的 **每个** 模块。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_FLAGS](../../../extensibility/debugger/reference/module-flags.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
