---
description: 此方法在给定名称后查找别名。
title: IDebugBinder3：：FindAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8138d702fb8507cfb1da24f28995b2bc4d21341f
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119901"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
此方法在给定名称后查找别名。 这将搜索程序的所有别名。

## <a name="syntax"></a>语法

```cpp
HRESULT FindAlias(
   LPCOLESTR     pcstrName,
   IDebugAlias** ppAlias
);
```

```csharp
int FindAlias(
   string          pcstrName,
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>参数
`pcstrName`\
[in]要查找的别名。

`ppAlias`\
[out]如果任何 ([IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 接口) ，则找到别名。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则，如果 (`S_FALSE` 别名或错误代码) ，则 返回 。

## <a name="remarks"></a>备注
 此方法在调用 之前将目标对象初始化为 null;然后，它会测试 null 值，以确定是否找到别名。

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
