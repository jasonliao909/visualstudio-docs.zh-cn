---
description: 加载 (调试) 调试的所有模块的符号。
title: IDebugEngine3：：LoadSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b1faedbca01e1e37ef50894526a7c775205ea215
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664842"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
加载 (调试) 调试的所有模块的符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>parameters
 无。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则返回错误代码。

## <a name="remarks"></a>备注
 这会加载此调试引擎引用的所有模块的调试符号。 只有在尚未加载符号时，才加载符号。 通过调用 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)在设置的路径上搜索符号。

## <a name="see-also"></a>另请参阅
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
