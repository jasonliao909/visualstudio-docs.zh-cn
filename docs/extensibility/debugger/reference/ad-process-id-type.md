---
description: 指定如何解释 AD_PROCESS_ID 结构中的进程 ID。
title: AD_PROCESS_ID_TYPE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AD_PROCESS_ID_TYPE
helpviewer_keywords:
- AD_PROCESS_ID_TYPE enumeration
ms.assetid: 0aab80e9-285a-4697-94ac-c864d42a6aaa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 97187d49f73e53967ad172406d22073341822fbf
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122120525"
---
# <a name="ad_process_id_type"></a>AD_PROCESS_ID_TYPE
指定如何解释 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 结构中的进程 ID。

## <a name="syntax"></a>语法

```cpp
enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
typedef DWORD AD_PROCESS_ID_TYPE;
```

```csharp
public enum enum_AD_PROCESS_ID {
    AD_PROCESS_ID_SYSTEM = 0,
    AD_PROCESS_ID_GUID   = 1
};
```

## <a name="fields"></a>字段
`AD_PROCESS_ID_SYSTEM`\
进程 ID 是系统标识符。 使用 `ProcessId.dwProcessId` [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 结构的字段。

`AD_PROCESS_ID_GUID`\
进程 ID 是一个 GUID。 使用 `ProcessId.guidProcessId` 结构的字段 `AD_PROCESS_ID` 。

## <a name="remarks"></a>备注
用于 `ProcessIdType` [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 结构的成员，以确定结构中包含的进程 ID 的类型。 确定如何解释 `ProcessId` 结构中的联合。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)
