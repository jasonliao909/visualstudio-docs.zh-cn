---
title: IDebugProgramNode2：:D etachDebugger_V7 |Microsoft Docs
description: 此方法是 2005 年 5 月之前使用的分离方法的旧式Visual Studio形式。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::DetachDebugger
helpviewer_keywords:
- IDebugProgramNode2::DetachDebugger
- IDebugProgramNode2::DetachDebugger_V7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 77d3d076df7bef55f0c68040d578b4627bdfe030e7118bec37497ac98d65d143
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449217"
---
# <a name="idebugprogramnode2detachdebugger_v7"></a>IDebugProgramNode2::DetachDebugger_V7

> [!Note]
> 废弃。 请勿使用。

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

实现应始终返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 从 Visual Studio 2005 起，不再使用此方法，应始终返回 `E_NOTIMPL` 。

当调试器意外退出时，将调用此方法。 调用此方法时，DE 应像用户分离程序一样恢复程序。 不应再发送调试事件。 程序应位于从调试器的另一个实例附加的状态。

## <a name="see-also"></a>另请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
