---
description: 返回模块枚举中的下一组元素。
title: IEnumDebugModules2：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2::Next
helpviewer_keywords:
- IEnumDebugModules2::Next
ms.assetid: 46b7ccad-b07b-4ec0-b3ce-13981ffab7e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a450a0a659b78fbe55a46098458a7e7370c4a10c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118211"
---
# <a name="ienumdebugmodules2next"></a>IEnumDebugModules2::Next
返回 枚举中的下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG           celt,
   IDebugModule2** rgelt,
   ULONG*          pceltFetched
);
```

```csharp
int Next(
   uint            celt,
   IDebugModule2[] rgelt,
   ref uint        pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 还指定数组的最大 `rgelt` 大小。

`rgelt`\
[in， out]要填充 [的 IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 元素的数组。

`pceltFetched`\
[out]返回 中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果可能返回的元素数少于请求的元素数，则返回 `S_FALSE` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
