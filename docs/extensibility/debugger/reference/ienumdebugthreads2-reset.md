---
description: 将线程枚举重置为第一个元素。
title: IEnumDebugThreads2：：Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::Reset
helpviewer_keywords:
- IEnumDebugThreads2::Reset
ms.assetid: 88980d9a-c4d6-4de4-a9ab-fb56fa71394a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9fc6b0f2e4dd25657d08ac1c5d814097c885c392
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103229"
---
# <a name="ienumdebugthreads2reset"></a>IEnumDebugThreads2::Reset
将枚举重置为第一个元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Reset(
   void
);
```

```csharp
int Reset();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，对 [Next](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md) 方法的下一次调用将返回 枚举的第一个元素。

## <a name="see-also"></a>请参阅
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
