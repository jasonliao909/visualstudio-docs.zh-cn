---
description: 检索表示新创建的调试引擎 (DE) 的对象。
title: IDebugEngineCreateEvent2：： GetEngine |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineCreateEvent2::GetEngine
helpviewer_keywords:
- IDebugEngineCreateEvent2::GetEngine
ms.assetid: 187d24ed-9f9a-4418-a0ef-b8a19f54652c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66e58c94f21eb29b7cb85066001e5c4472730f76
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066082"
---
# <a name="idebugenginecreateevent2getengine"></a>IDebugEngineCreateEvent2::GetEngine
检索表示新创建的调试引擎 (DE) 的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngine( 
   IDebugEngine2** pEngine
);
```

```csharp
int GetEngine( 
   out IDebugEngine2 pEngine
);
```

## <a name="parameters"></a>参数
`pEngine`\
弄返回一个 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 对象，该对象表示新创建的 DE。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
