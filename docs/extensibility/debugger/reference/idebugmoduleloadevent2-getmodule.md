---
description: 获取正在加载或卸载的模块。
title: IDebugModuleLoadEvent2：： GetModule |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2::GetModule
helpviewer_keywords:
- IDebugModuleLoadEvent2::GetModule
ms.assetid: c86482bb-9ce5-4e63-bbe0-969b50169424
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4605b5eab9137fd918238143d8f0453f9f8c54b8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065367"
---
# <a name="idebugmoduleloadevent2getmodule"></a>IDebugModuleLoadEvent2::GetModule
获取正在加载或卸载的模块。

## <a name="syntax"></a>语法

```cpp
HRESULT GetModule( 
   IDebugModule2** pModule,
   BSTR*           pbstrDebugMessage,
   BOOL*           pbLoad
);
```

```csharp
int GetModule( 
   out IDebugModule2 pModule,
   ref string        pbstrDebugMessage,
   ref int           pbLoad
);
```

## <a name="parameters"></a>参数
`pModule`\
弄返回一个 [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) 对象，该对象表示正在加载或卸载的模块。

`pbstrDebugMessage`\
[in，out]返回描述此事件的可选消息。 如果此参数为 null 值，则不请求消息。

`pbLoad`\
[in，out]如果模块正在加载，则为非零 (`TRUE`)  () ，则为 `FALSE` 。 如果此参数为 null 值，则不请求状态。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
