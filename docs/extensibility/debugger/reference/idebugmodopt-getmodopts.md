---
description: 检索可选修饰符的列表。
title: IDebugModOpt：： GetModOpts |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt::GetModOpts
- GetModOpts
ms.assetid: cb513fa9-d521-4a65-b968-f55f53a368df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f2774fa214e36669dcdb9190d57dddc095696d88
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043331"
---
# <a name="idebugmodoptgetmodopts"></a>IDebugModOpt::GetModOpts
检索可选修饰符的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetModOpts(
   ULONG  celt,
   BSTR*  rgelt,
   ULONG* pceltFetched
);
```

```csharp
int GetModOpts(
   uint         celt,
   out string[] rgelt,
   ref uint     pceltFetched
);
```

## <a name="parameters"></a>参数
`celt`\
中要返回的元素的数目。

`rgelt`\
弄返回一个包含选项的数组。

`pceltFetched`\
[in，out]在数组中返回的元素的数目 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)
