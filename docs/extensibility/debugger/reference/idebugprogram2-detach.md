---
title: IDebugProgram2：:D etach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Detach
helpviewer_keywords:
- IDebugProgram2::Detach
ms.assetid: 5e8d88b0-a8d4-4746-88c0-ad332ee73f33
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3ba312ce18dd0a3ee2bbf65d83390a2af9f4ac3d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912930"
---
# <a name="idebugprogram2detach"></a>IDebugProgram2::Detach
从程序分离调试引擎。

## <a name="syntax"></a>语法

```cpp
HRESULT Detach( 
   void 
);
```

```csharp
int Detach();
```

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 分离的程序将继续运行，但不再是调试会话的一部分。 分离调试引擎后，不会再发送程序调试事件。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
