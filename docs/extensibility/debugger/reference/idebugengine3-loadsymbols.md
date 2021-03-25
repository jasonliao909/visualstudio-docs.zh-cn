---
description: 将 (加载到此调试引擎正在调试的所有模块的必要) 符号。
title: IDebugEngine3：： LoadSymbols |Microsoft Docs
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 43651baac29b3904b9bc12d8d4b965ca1cd8e3ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066173"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
将 (加载到此调试引擎正在调试的所有模块的必要) 符号。

## <a name="syntax"></a>语法

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 这会为此调试引擎所引用的所有模块加载调试符号。 仅在未加载符号时才加载它们。 在通过调用 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)设置的路径上搜索符号。

## <a name="see-also"></a>另请参阅
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
