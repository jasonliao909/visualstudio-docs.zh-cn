---
description: 返回进程枚举中的下一组元素。
title: IEnumDebugProcesses2：： Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugProcesses2::Next
helpviewer_keywords:
- IEnumDebugProcesses2::Next
ms.assetid: abef89eb-198b-49cd-a4c9-17bce6cac0e1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1a50343d2b57b602b8c87578595fa21f8aef7754
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664429"
---
# <a name="ienumdebugprocesses2next"></a>IEnumDebugProcesses2::Next
返回枚举中的下一个元素集。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProcess2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProcess2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>parameters
`celt`\
中要检索的元素的数目。 还指定数组的最大大小 `rgelt` 。

`rgelt`\
[in，out]要填充的 [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) 元素的数组。

`pceltFetched`\
弄返回中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果返回的元素数少于所请求的数目，则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IEnumDebugProcesses2](../../../extensibility/debugger/reference/ienumdebugprocesses2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
