---
description: 获取 DE (接口) 调试引擎。
title: IDebugQueryEngine2：：GetEngineInterface |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5458ec92e121fcfe954e03a660370ec207d3ba55
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664471"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
获取 DE (接口) 调试引擎。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInterface( 
   IUnknown** ppUnk
);
```

```csharp
int GetEngineInterface( 
   out object ppUnk
);
```

## <a name="parameters"></a>parameters
`ppUnk`\
[out]返回一个 对象，该对象表示调试引擎 (DE) ，可以查询该引擎，以查询与 DE (关联的任何其他有效接口 `IUnknown` ，例如 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 或 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)) 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 应谨慎使用生成的接口，因为通过从此方法检索的接口调用 会绕过会话调试管理器的处理，并且可能会导致 SDM 在调试时进入错误状态或生成错误。

## <a name="see-also"></a>另请参阅
- [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
