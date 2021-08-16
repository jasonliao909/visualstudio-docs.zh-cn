---
description: 检索可用调试引擎的唯一标识符数组。
title: IDebugProcess3：：GetEngineFilter |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetEngineFilter
- IDebugProcess3::GetEngineFilter
ms.assetid: ccb7ecb0-f189-4e80-b5b2-221a095e01f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bcb04ed408d0ed3947bd7b31f0eaa8876fa329339ff431bcdb25e5f08b91b812
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276693"
---
# <a name="idebugprocess3getenginefilter"></a>IDebugProcess3::GetEngineFilter
检索可用调试引擎的唯一标识符数组。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineFilter(
   GUID_ARRAY *pEngineArray
);
```

```csharp
public int GetEngineFilter(
   out GUID_ARRAY[] pEngineArray
);
```

## <a name="parameters"></a>参数
`pEngineArray`\
[out]对包含调试引擎的唯一标识符的结构的引用。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md)
