---
description: 为当前模块加载符号。
title: IDebugModule3：： LoadSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3::LoadSymbols
helpviewer_keywords:
- IDebugModule3::LoadSymbols
ms.assetid: 7548c8c1-cbc6-48aa-a845-19058d4a85bb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ca735fe22c1bcb8aca5ae4150df7d4606c508e5
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122043279"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
为当前模块加载符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbols(
   void
);
```

```csharp
int LoadSymbols();
```

## <a name="return-value"></a>返回值
 如果该方法成功，则它会返回 `S_OK`。 如果该方法失败，则会返回错误代码。

## <a name="remarks"></a>备注
 此方法从当前搜索路径加载符号 (可以通过调用 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md) 方法) 来更改该符号。

 此方法优于 [ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
