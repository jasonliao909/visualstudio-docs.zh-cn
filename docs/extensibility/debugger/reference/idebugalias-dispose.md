---
description: 将此别名标记为删除。
title: IDebugAlias：:D ispose |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: efca2b2bedc531fa241d8cfe6cfe8cd3527a7b40
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143917"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
将此别名标记为删除。

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
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 调用此方法后，该别名将不再可用。

## <a name="see-also"></a>另请参阅
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
