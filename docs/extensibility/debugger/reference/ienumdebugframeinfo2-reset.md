---
description: 将枚举重置为第一个 FRAMEINFO 元素。
title: IEnumDebugFrameInfo2：：Reset |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2::Reset
helpviewer_keywords:
- IEnumDebugFrameInfo2::Reset
ms.assetid: e149b559-f072-480b-9552-a452b147f3a8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f831ec32a51115dd1a7527e4b1a9ee3a41b93ea30549aba91a86f4113d54983b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415216"
---
# <a name="ienumdebugframeinfo2reset"></a>IEnumDebugFrameInfo2::Reset
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
 调用此方法后，对 [Next](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md) 方法的下一次调用将返回 枚举的第一个元素。

## <a name="see-also"></a>另请参阅
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
