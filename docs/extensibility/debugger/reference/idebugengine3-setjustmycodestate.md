---
description: 此方法告知调试引擎 JustMyCode 状态信息。
title: IDebugEngine3：：SetJustMyCodeState |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fb528d3f8c12e21f327b168a88d4df070e2863188fcc8e1580135db9685c1ca4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121307773"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
此方法告知调试引擎 JustMyCode 状态信息。

## <a name="syntax"></a>语法

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>参数
`fUpdate`\
[in]非零 () 更新当前信息，零 () 重置所有信息 (忽略之前设置 `TRUE` `FALSE`) 。

`dwModules`\
[in]中的信息结构数 `rgJMCSpec.`

`rgJMCSpec`\
[in]要JMC_CODE_SPEC [的](../../../extensibility/debugger/reference/jmc-code-spec.md) 数组。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 JustMyCode 是仅调试属于用户的代码并忽略所有中间代码（如系统代码）的概念，即使源代码可用于该系统代码。

## <a name="see-also"></a>另请参阅
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
