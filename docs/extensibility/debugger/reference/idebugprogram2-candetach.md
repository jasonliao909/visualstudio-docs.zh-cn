---
description: 确定调试引擎 (DE) 是否可以与程序分离。
title: IDebugProgram2：： CanDetach |Microsoft Docs
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e751429fe26060a515f94aa3d402954ff598d39
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076168"
---
# <a name="idebugprogram2candetach"></a>IDebugProgram2::CanDetach
确定调试引擎 (DE) 是否可以与程序分离。

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
 如果可以分离， `S_OK` 则返回; 否则返回错误代码。 `S_FALSE`如果 DE 无法与程序分离，则返回。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
