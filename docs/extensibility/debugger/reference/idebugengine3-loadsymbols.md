---
title: IDebugEngine3：： LoadSymbols |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f823f0087ee612a7850e000469271e0c2a778b62
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887297"
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

## <a name="parameters"></a>parameters
 无。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 这会为此调试引擎所引用的所有模块加载调试符号。 仅在未加载符号时才加载它们。 在通过调用 [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)设置的路径上搜索符号。

## <a name="see-also"></a>另请参阅
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
