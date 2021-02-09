---
title: IDebugProgramNode2：:D etachDebugger_V7 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0593a2ee8c519169bd8cb2eb23a83c4f5f3506a0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898629"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 弃用. 请勿使用。

## <a name="syntax"></a>语法

```cpp
HRESULT DetachDebugger_V7 (
   void 
);
```

```csharp
int DetachDebugger_V7 ();
```

## <a name="return-value"></a>返回值

实现应总是返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 在 Visual Studio 2005 中，此方法不再使用，应始终返回 `E_NOTIMPL` 。

当调试器意外退出时，将调用此方法。 调用此方法时，DE 应恢复程序，就像用户将其分离一样。 不应发送更多调试事件。 程序应处于可从调试器的另一个实例中附加的状态。

## <a name="see-also"></a>另请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
