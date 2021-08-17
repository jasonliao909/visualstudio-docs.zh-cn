---
description: 检索可选修饰符的列表。
title: IDebugModOpt：：GetModOpts |Microsoft Docs
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
ms.openlocfilehash: c13c664e80fe0ea2d479911d75fbd62b5d51e97b143fcd1cd89144718a5ede86
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433627"
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
[in]要返回的元素数。

`rgelt`\
[out]返回包含选项的数组。

`pceltFetched`\
[in， out]数组中返回的元素 `rgelt` 数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugModOpt](../../../extensibility/debugger/reference/idebugmodopt.md)
