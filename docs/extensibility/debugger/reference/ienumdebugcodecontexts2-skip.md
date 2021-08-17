---
description: 跳过代码上下文枚举中的指定元素数。
title: IEnumDebugCodeContexts2：：Skip |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Skip
helpviewer_keywords:
- IEnumDebugCodeContexts2::Skip
ms.assetid: 3451a3eb-bf5b-4ec5-acc9-aa5a24363801
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1c0f47e57d4c3820f158c833649dc15f9f3c0e54
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029497"
---
# <a name="ienumdebugcodecontexts2skip"></a>IEnumDebugCodeContexts2::Skip
跳过指定数量的元素。

## <a name="syntax"></a>语法

```cpp
HRESULT Skip(
   ULONG celt
);
```

```csharp
int Skip(
   uint celt
);
```

## <a name="parameters"></a>参数
`celt`\
[in]要跳过的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果 `S_FALSE` `celt` 大于剩余元素的数量，则返回 ;否则返回错误代码。

## <a name="remarks"></a>备注
 如果 `celt` 指定一个大于剩余元素数的值，则枚举将设置为末尾并 `S_FALSE` 返回 。

## <a name="see-also"></a>请参阅
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
