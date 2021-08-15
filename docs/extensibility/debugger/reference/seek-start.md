---
description: 指定开始在反汇编流中寻找的位置。
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
ms.openlocfilehash: 580c52a3df54f32beba45b4f44c1062e7197f766ae1ae9d25db6da29099537f2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433016"
---
# <a name="seek_start"></a>SEEK_START
指定开始在反汇编流中寻找的位置。

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
 从当前文档的开头开始寻找。

 `SEEK_START_END`\
 在当前文档的末尾开始寻找。

 `SEEK_START_CURRENT`\
 从当前文档的当前位置开始寻找。

 `SEEK_START_CODECONTEXT`\
 开始在当前文档的给定代码上下文中进行寻找。

 `SEEK_START_CODELOCID`\
 开始在给定的代码位置标识符处进行寻找。 通过调用 [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)获取代码位置标识符。

## <a name="remarks"></a>备注
 作为参数传递给 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md) 方法。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
