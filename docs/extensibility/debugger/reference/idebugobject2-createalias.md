---
description: 为此对象创建唯一的 ID 或别名，或返回现有别名。
title: IDebugObject2：： CreateAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::CreateAlias
helpviewer_keywords:
- IDebugObject2::CreateAlias method
ms.assetid: 54a05920-5d13-4f67-962b-d1a7f013dff9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ce75ad8f1b6e8bac1cc61281fef8b7dbbb268a2cd5121644f40822334eda1d66
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417010"
---
# <a name="idebugobject2createalias"></a>IDebugObject2::CreateAlias
为此对象创建唯一的 ID 或别名，或返回现有别名。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int CreateAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>参数
`ppAlias`\
弄新的 (或现有的) 别名。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 别名是一个标签，表示对象在内存中的特定对象。

## <a name="see-also"></a>请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
