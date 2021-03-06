---
description: 此方法创建可视化工具服务。
title: IEEVisualizerServiceProvider：： CreateVisualizerService |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService
helpviewer_keywords:
- IEEVisualizerServiceProvider::CreateVisualizerService method
ms.assetid: f366f7c9-358d-46c8-993f-32ff86539833
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b304dd8fe2845cf6c1201e6e128f8b89ec47b1b6
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222817"
---
# <a name="ieevisualizerserviceprovidercreatevisualizerservice"></a>IEEVisualizerServiceProvider::CreateVisualizerService
此方法创建可视化工具服务。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateVisualizerService(
   IDebugBinder*              binder,
   IDebugSymbolProvider*      pSymProv,
   IDebugAddress*             pAddress,
   IEEVisualizerDataProvider* dataProvider,
   IEEVisualizerService**     ppService
);
```

```csharp
int CreateVisualizerService(
   IDebugBinder binder,
   IDebugSymbolProvider      pSymProv,
   IDebugAddress             pAddress,
   IEEVisualizerDataProvider dataProvider,
   out IEEVisualizerService  ppService
);
```

## <a name="parameters"></a>参数
`binder`\
中传递给[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。

`pSymProv`\
中传递给的 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 对象 `IDebugParsedExpression::EvaluateSync` 。

`pAddress`\
中传递给的 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象 `IDebugParsedExression::EvaluateSync` 。

`dataProvider`\
中实现 [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) 接口的对象 (由表达式计算器) 提供。

`ppService`\
弄创建的服务。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 `binder`、 `pSymProv` 和参数都 `pAddress` 传递给 `IDebugParsedExpression::EvaluateSync` 方法。 `CreateVisualizerService` 仅 `IDebugParsedExpression::EvaluateSync` 作为表达式计算器对类型可视化工具的支持的一部分进行调用。

## <a name="see-also"></a>请参阅
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
