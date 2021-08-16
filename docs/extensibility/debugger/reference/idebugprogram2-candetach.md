---
description: 确定调试引擎 (DE) 能否与程序分离。
title: IDebugProgram2：：CanDetach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::CanDetach
helpviewer_keywords:
- IDebugProgram2::CanDetach
ms.assetid: dcd9ab6c-49e5-447e-aa7c-89f571f4a052
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 45d4bef36f5b1e283d654bcee4b6eaac09becd6b7f9ffe54f969f78f6ef1f655
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276602"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
确定调试引擎 (DE) 能否与程序分离。

## <a name="syntax"></a>语法

```cpp
HRESULT CanDetach(
   void
);
```

```csharp
int CanDetach();
```

## <a name="return-value"></a>返回值
 如果 可以分离，则 返回 `S_OK` ;否则返回错误代码。 如果 `S_FALSE` DE 无法从程序分离，则返回 。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
