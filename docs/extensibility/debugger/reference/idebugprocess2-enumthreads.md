---
description: 检索进程中运行的所有线程的列表。
title: IDebugProcess2：： EnumThreads |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumThreads
helpviewer_keywords:
- IDebugProcess2::EnumThreads
ms.assetid: 05677385-7a7f-4545-8438-af00dde85db0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c17457429f83ae012e12cdc6bf7ff1448cd74989afe52f870c52f75b4446e824
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339029"
---
# <a name="idebugprocess2enumthreads"></a>IDebugProcess2::EnumThreads
检索进程中运行的所有线程的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumThreads(
   IEnumDebugThreads2** ppEnum
);
```

```csharp
int EnumThreads(
   out IEnumDebugThreads2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回一个 [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md) 对象，该对象包含进程的所有程序中的所有线程的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法枚举在每个程序中运行的线程，然后将它们合并到线程的进程视图中。 单个线程可能会在多个程序中运行;此方法只枚举一次该线程。

 此方法显示进程的线程列表（不包含重复项）。 否则，若要枚举在特定程序中运行的线程，请使用 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
