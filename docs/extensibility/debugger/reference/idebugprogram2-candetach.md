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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69bd7950d5b0cb884b8f59ae309265a0273d0944
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166068"
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
