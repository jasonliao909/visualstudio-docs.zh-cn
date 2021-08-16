---
description: 加载当前模块的符号。
title: IDebugModule3：：LoadSymbols |Microsoft Docs
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
ms.openlocfilehash: 2b332182574f9801f1a1ef6eb139d46958851d725191bc1355f800c8161b1183
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307292"
---
# <a name="idebugmodule3loadsymbols"></a>IDebugModule3::LoadSymbols
加载当前模块的符号。

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
 此方法从当前搜索路径加载符号 (调用 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md) 方法) 。

 此方法比方法[ReloadSymbols_Deprecated首选。](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)

## <a name="see-also"></a>另请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
