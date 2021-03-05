---
description: 此方法在给定名称的情况下查找别名。
title: IDebugBinder3：： FindAlias |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::FindAlias
helpviewer_keywords:
- IDebugBinder3::FindAlias method
ms.assetid: b8333701-2718-4983-8513-0875fb7cb730
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db4d5cad6d0c2990141e0dd3a824425b8b53145b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167719"
---
# <a name="idebugbinder3findalias"></a>IDebugBinder3::FindAlias
此方法在给定名称的情况下查找别名。 这会搜索程序中的所有别名。

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
中要查找的别名的名称。

`ppAlias`\
弄如果 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 接口所表示的任何)  (，则会找到别名。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则， `S_FALSE` 如果找不到别名) 或错误代码，则返回 (。

## <a name="remarks"></a>备注
 此方法在调用之前将目标对象初始化为 null;然后，它将在此后测试 null 值，以确定是否找到了别名。

## <a name="see-also"></a>另请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
