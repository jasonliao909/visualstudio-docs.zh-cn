---
description: 获取此调试事件的属性。
title: IDebugEvent2：：GetAttributes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEvent2::GetAttributes
helpviewer_keywords:
- IDebugEvent2::GetAttributes
ms.assetid: 2ac5b5fb-da17-43f7-811a-313f677e60d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba1b39a74497633e7a6cd1a2655b83550ae3a51c
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602408"
---
# <a name="idebugevent2getattributes"></a>IDebugEvent2::GetAttributes
获取此调试事件的属性。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAttribute( 
   DWORD* pdwAttrib
);
```

```csharp
int GetAttribute( 
   out uint pdwAttrib
);
```

## <a name="parameters"></a>parameters
`pdwAttrib`\
[out] [EVENTATTRIBUTES 枚举中标志](../../../extensibility/debugger/reference/eventattributes.md) 的组合。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)接口对于所有事件都是通用的。 此方法描述事件的类型;例如， 是同步或异步事件，是停止事件。

## <a name="see-also"></a>另请参阅
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [EVENTATTRIBUTES](../../../extensibility/debugger/reference/eventattributes.md)
