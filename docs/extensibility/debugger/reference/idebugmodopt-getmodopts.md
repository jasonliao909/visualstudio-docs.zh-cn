---
title: IDebugModOpt：： GetModOpts |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt::GetModOpts
- GetModOpts
ms.assetid: cb513fa9-d521-4a65-b968-f55f53a368df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 78ddcaa6a062b844c3f60c04f7a08aa673c69f67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99941783"
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

## <a name="parameters"></a>parameters
`celt`\
中要返回的元素的数目。

`rgelt`\
弄返回一个包含选项的数组。

`pceltFetched`\
[in，out]在数组中返回的元素的数目 `rgelt` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)
