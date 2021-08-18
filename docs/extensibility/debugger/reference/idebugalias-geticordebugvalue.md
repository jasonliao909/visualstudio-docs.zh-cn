---
description: 检索表示与此别名关联的值的托管代码接口。
title: IDebugAlias：： GetICorDebugValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 223414a7fea10f14fdc8e8c9d71f5b3dbb036ba2
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122104412"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
检索表示与此别名关联的值的托管代码接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetICorDebugValue(
   IUnknown** ppUnk
);
```

```csharp
int GetICorDebugValue(
   out object ppUnk
);
```

## <a name="parameters"></a>参数
`ppUnk`\
[out] `IUnknown` 表示与此别名关联的值的接口。 可以查询此接口的接口 `ICorDebugValue` 。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 此方法仅适用于托管值 (`ICorDebugValue` 是 .NET Framework 中可用的接口，并且在 cordebug.idl 文件) 的 .NET Framework SDK 中定义。

## <a name="see-also"></a>请参阅
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
