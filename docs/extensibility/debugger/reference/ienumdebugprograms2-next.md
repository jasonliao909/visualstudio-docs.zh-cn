---
description: 返回程序枚举中的下一组元素。
title: IEnumDebugPrograms2：：Next |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2::Next
helpviewer_keywords:
- IEnumDebugPrograms2::Next
ms.assetid: 9120e263-e97c-4a40-ab2c-e9264ce3d6c4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 74d604df42779755093518472b0d70d0983c0da9c39ad2e559eeac5cc087f324
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415229"
---
# <a name="ienumdebugprograms2next"></a>IEnumDebugPrograms2::Next
返回 枚举中的下一组元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Next(
   ULONG            celt,
   IDebugProgram2** rgelt,
   ULONG*           pceltFetched
);
```

```csharp
int Next(
   uint             celt,
   IDebugProgram2[] rgelt,
   ref uint         pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要检索的元素数。 还指定数组的最大 `rgelt` 大小。

`rgelt`\
[in， out]要填充 [的 IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) 元素的数组。

`pceltFetched`\
[out]返回 中实际返回的元素数 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果可能返回的元素数少于请求的元素数，则返回 `S_FALSE` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
