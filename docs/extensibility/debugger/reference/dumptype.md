---
description: 指定要转储的程序状态 (，例如正在运行的线程、堆栈帧和当前) 地址。
title: DUMPTYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DUMPTYPE
helpviewer_keywords:
- DUMPTYPE enumeration
ms.assetid: ea8160db-8732-4056-a1d7-892ef72da71e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3054d86c1d516f79cbf259eaaf4add7ae1befc51
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104620"
---
# <a name="dumptype"></a>DUMPTYPE
指定要转储的程序状态 (，例如正在运行的线程、堆栈帧和当前) 地址。

## <a name="syntax"></a>语法

```cpp
enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
typedef DWORD DUMPTYPE;
```

```csharp
public enum enum_DUMPTYPE {
    DUMP_MINIDUMP = 0,
    DUMP_FULLDUMP = 1
};
```

## <a name="fields"></a>字段
`DUMP_MINIDUMP`\
指定小型压缩转储。

`DUMP_FULLDUMP`\
指定大型的完整转储。

## <a name="remarks"></a>备注
作为参数传递给 [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md) 方法。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [WriteDump](../../../extensibility/debugger/reference/idebugprogram2-writedump.md)
