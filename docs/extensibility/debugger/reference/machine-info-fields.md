---
description: 指定要为特定计算机检索的信息类型。
title: MACHINE_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MACHINE_INFO_FIELDS
helpviewer_keywords:
- MACHINE_INFO_FIELDS enumeration
ms.assetid: 2d61d206-7d40-4df1-8c88-1b3c9c78821e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 448edb134ba6065c85ee1547c73f45f9df769563
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103138"
---
# <a name="machine_info_fields"></a>MACHINE_INFO_FIELDS
指定要为特定计算机检索的信息类型。

## <a name="syntax"></a>语法

```cpp
enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
typedef DWORD MACHINE_INFO_FIELDS;
```

```csharp
public enum enum_MACHINE_INFO_FIELDS { 
   MCIF_NAME  = 0x00000001,
   MCIF_FLAGS = 0x00000002,
   MCIF_ALL   = 0x00000003
};
```

## <a name="fields"></a>字段
 `MCIF_NAME`\
 初始化/使用 `bstrName` 结构中的字段。

 `MCIF_FLAGS`\
 初始化/使用 `Flags` 结构中的字段。

 `MIF_ALL`\
 初始化/使用结构中的所有字段。

## <a name="remarks"></a>备注
 这些值将传递给 [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md) 方法，以指示要初始化 [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md) 结构的哪些成员。

 还在结构的 `Fields` 成员中用于 `MACHINE_INFO` 指示哪些字段已使用并且有效。

 这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)
- [GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)
