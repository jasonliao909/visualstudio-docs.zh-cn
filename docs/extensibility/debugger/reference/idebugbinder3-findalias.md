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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 99d015fa327992f22fbab95513102ed9e376a96a29a6ae037ac8f33acb2ea30b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403008"
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

## <a name="see-also"></a>请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
