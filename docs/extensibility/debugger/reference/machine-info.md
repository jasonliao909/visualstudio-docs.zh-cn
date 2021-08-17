---
description: 描述特定计算机。
title: MACHINE_INFO |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO
helpviewer_keywords:
- MACHINE_INFO structure
ms.assetid: e7564ff2-00b5-4750-8fd5-dc1029a16912
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b59699c5ec284c2bb1d9534de8960b7706c1804ea95310f1a14b93fd7085d472
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121401851"
---
# <a name="machine_info"></a>MACHINE_INFO
描述特定计算机。

## <a name="syntax"></a>语法

```cpp
typedef struct tagMACHINE_INFO { 
   MACHINE_INFO_FIELDS Fields;
   BSTR                bstrName;
   MACHINE_INFO_FLAGS  Flags;
} MACHINE_INFO;
```

```csharp
public struct MACHINE_INFO { 
   public uint   Fields;
   public string bstrName;
   public uint   Flags;
};
```

## <a name="members"></a>成员
 `Fields`\
 集合中标志的组合 [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md) 枚举，用于指定初始化结构的哪些字段。

 `bstrName`\
 计算机名称。 等效于调用 [GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)。

 `Flags`\
 描述计算机 [属性MACHINE_INFO_FLAGS集合](../../../extensibility/debugger/reference/machine-info-flags.md) 中的标志组合。

## <a name="remarks"></a>备注
 此结构通过调用 [GetMachineInfo 方法](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md) 返回。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [MACHINE_INFO_FIELDS](../../../extensibility/debugger/reference/machine-info-fields.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
