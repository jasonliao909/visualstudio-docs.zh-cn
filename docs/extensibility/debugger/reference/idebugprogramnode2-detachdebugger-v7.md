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
ms.openlocfilehash: 47ad13cc0f3f01665535e6b9d8168af79eb299f0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029978"
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
> 从 Visual Studio 2005 起，此方法不再使用，应始终返回 `E_NOTIMPL` 。

当调试器意外退出时，将调用此方法。 调用此方法时，DE 应像用户分离程序一样恢复程序。 不应再发送调试事件。 程序应位于从调试器的另一个实例附加的状态。

## <a name="see-also"></a>请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
