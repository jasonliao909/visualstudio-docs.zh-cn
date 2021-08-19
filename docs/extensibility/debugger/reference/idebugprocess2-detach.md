---
description: 通过分离进程中的所有程序，将调试器与此进程分离。
title: IDebugProcess2：:D etach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Detach
helpviewer_keywords:
- IDebugProcess2::Detach
ms.assetid: ee2b9084-2db1-4e49-a1d9-387284b7c3f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 44e45fa717f1292b57626df3fc68f90c8f0a9639
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126721"
---
# <a name="idebugprocess2detach"></a>IDebugProcess2::Detach
通过分离进程中的所有程序，将调试器与此进程分离。

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
 所有程序和进程都将继续运行，但不再是调试会话的一部分。 分离操作完成后，不会再发送此进程 (的调试事件，) 将发送其程序。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
