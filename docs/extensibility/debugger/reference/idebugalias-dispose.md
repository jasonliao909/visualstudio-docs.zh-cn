---
description: 标记此别名以删除。
title: IDebugAlias：:D pose |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e15d2c6f74c4872c5e55c9ce76293a1ab097d3176be33843a4deea89a692664c
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434212"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
标记此别名以删除。

## <a name="syntax"></a>语法

```cpp
HRESULT Dispose();
```

```csharp
int Dispose();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，别名将不再可用。

## <a name="see-also"></a>另请参阅
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
