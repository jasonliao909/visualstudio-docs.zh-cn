---
description: 指定步进的步骤类型。
title: STEPKIND |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- STEPKIND
helpviewer_keywords:
- STEPKIND enumeration
ms.assetid: d3d8cf76-24bf-455e-803e-0e3e28f0b262
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 521a185b3733ef8f5c4f862b992d1953031fd5fb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122110769"
---
# <a name="stepkind"></a>STEPKIND
指定步进的步骤类型。

## <a name="syntax"></a>语法

```cpp
enum enum_STEPKIND { 
   STEP_INTO      = 0,
   STEP_OVER      = 1,
   STEP_OUT       = 2,
   STEP_BACKWARDS = 3
};
typedef DWORD STEPKIND;
```

```csharp
public enum enum_STEPKIND { 
   STEP_INTO      = 0,
   STEP_OVER      = 1,
   STEP_OUT       = 2,
   STEP_BACKWARDS = 3
};
```

## <a name="fields"></a>字段
 `STEP_INTO`\
 执行函数的步骤。

 `STEP_OVER`\
 逐过程执行函数。

 `STEP_OUT`\
 跳出函数。

 `STEP_BACKWARDS`\
 向后移动到函数。

## <a name="remarks"></a>备注
 作为参数传递到 [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md) 方法。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)
