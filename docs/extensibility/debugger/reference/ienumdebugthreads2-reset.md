---
description: 将线程枚举重置为第一个元素。
title: IEnumDebugThreads2：： Reset |Microsoft Docs
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
ms.openlocfilehash: 74471161305f4fe9487f245cf578470e02f5fd2c4ecd2b26cc8e578880c849ff
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306512"
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
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后， [下一次调用的方法将](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md) 返回枚举的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
