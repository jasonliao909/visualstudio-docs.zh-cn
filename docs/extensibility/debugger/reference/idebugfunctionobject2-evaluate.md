---
description: IDebugFunctionObject2：：计算调用函数并将生成的值作为对象返回。
title: IDebugFunctionObject2：：求值 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86139b29b08fde8141dc905e98047a29520e6362
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088609"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
调用函数并将生成的值作为对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Evaluate (
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwEvalFlags,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate (
   IDebugObject     ppParams,
   uint             dwParams,
   uint             dwEvalFlags,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>参数
`ppParams`\
中表示输入参数的 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的数组。 其中每个参数都是通过使用此接口中的某个 Create 方法创建的。

`dwParams`\
中数组中参数的数目 `ppParams` 。

`dwEvalFlags`\
中 [EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md) 枚举中的标志的组合，该枚举指定如何执行计算。

`dwTimeout`\
中指定从此方法返回之前要等待的最长时间（以毫秒为单位）。 使用 **无限大** 无限期等待。

`ppResult`\
弄返回一个 **IDebugObject** ，它将函数的值表示为对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
