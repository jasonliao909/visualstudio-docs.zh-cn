---
description: 获取包含此类的类。
title: IDebugClassField：： GetEnclosingClass |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd6f6314afd1489609d5f93a44f3645cb70de8e8
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122072411"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
获取包含此类的类。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEnclosingClass(
    IDebugClassField** ppClassField
);
```

```csharp
int GetEnclosingClass(
    out IDebugClassField ppClassField
);
```

## <a name="parameters"></a>参数
`ppClassField`\
弄返回表示封闭类的 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象。 如果没有封闭类，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
如果此 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) 对象表示的类是嵌套类，则 `ppClassField` 参数将返回 `IDebugClassField` 表示封闭类的对象。 例如，给定此类定义：

```
class RootClass {
    class NestedClass { }
};
```

`GetEnclosingClass`在表示类的对象上调用方法将 `IDebugClassField` `NestedClass` 返回一个 `IDebugClassField` 表示类的对象 `RootClass` 。

## <a name="see-also"></a>请参阅
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
