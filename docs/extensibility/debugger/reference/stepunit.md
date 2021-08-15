---
description: 指定步进的步骤单元。
title: STEPUNIT |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- STEPUNIT
helpviewer_keywords:
- STEPUNIT enumeration
ms.assetid: cb8441f2-f744-4e73-acfe-ae8542df9649
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 48b9a6c4b008fe44dcfcbfe0599d871bc609513c79801510369b657eaa819b9c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448541"
---
# <a name="stepunit"></a>STEPUNIT
指定步进的步骤单元。

## <a name="syntax"></a>语法

```cpp
enum enum_STEPUNIT { 
   STEP_STATEMENT   = 0,
   STEP_LINE        = 1,
   STEP_INSTRUCTION = 2
};
typedef DWORD STEPUNIT;
```

```csharp
enum enum_STEPUNIT { 
   STEP_STATEMENT   = 0,
   STEP_LINE        = 1,
   STEP_INSTRUCTION = 2
};
```

## <a name="fields"></a>字段
 `STEP_STATEMENT`\
 步骤 by 语句。

 `STEP_LINE`\
 逐行。

 `STEP_INSTRUCTION`\
 按说明操作。

## <a name="remarks"></a>备注
 作为参数传递到 [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md) 方法。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)
