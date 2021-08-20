---
description: 指定在反汇编流中开始查找的位置。
title: SEEK_START |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- SEEK_START
helpviewer_keywords:
- SEEK_START enumeration
ms.assetid: 55bd8901-626e-428b-a263-23b14417f4c6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a7940ca7689da1dab20141191489800c2a3810c3
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122125226"
---
# <a name="seek_start"></a>SEEK_START
指定在反汇编流中开始查找的位置。

## <a name="syntax"></a>语法

```cpp
enum enum_SEEK_START { 
   SEEK_START_BEGIN       = 0x0001,
   SEEK_START_END         = 0x0002,
   SEEK_START_CURRENT     = 0x0003,
   SEEK_START_CODECONTEXT = 0x0004,
   SEEK_START_CODELOCID   = 0x0005
};
typedef DWORD SEEK_START;
```

```csharp
public enum enum_SEEK_START { 
   SEEK_START_BEGIN       = 0x0001,
   SEEK_START_END         = 0x0002,
   SEEK_START_CURRENT     = 0x0003,
   SEEK_START_CODECONTEXT = 0x0004,
   SEEK_START_CODELOCID   = 0x0005
};
```

## <a name="fields"></a>字段
 `SEEK_START_BEGIN`\
 开始在当前文档的开头进行查找。

 `SEEK_START_END`\
 开始在当前文档的末尾进行查找。

 `SEEK_START_CURRENT`\
 在当前文档的当前位置开始查找。

 `SEEK_START_CODECONTEXT`\
 开始在当前文档的给定代码上下文中查找。

 `SEEK_START_CODELOCID`\
 开始查找给定的代码位置标识符。 通过调用 [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)获取代码位置标识符。

## <a name="remarks"></a>备注
 作为参数传递给 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) 方法。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
