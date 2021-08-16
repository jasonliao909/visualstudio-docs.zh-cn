---
description: 描述代码中函数中断点的偏移位置。
title: BP_LOCATION_CODE_FUNC_OFFSET |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET
helpviewer_keywords:
- BP_LOCATION_CODE_FUNC_OFFSET structure
ms.assetid: ab38f7ca-fa01-4cf3-a06c-56cbb7207617
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: d30e83f11ea9227eb598efc27ae4852fcbf521e562873acff9f52eecd53b7eca
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121403258"
---
# <a name="bp_location_code_func_offset"></a>BP_LOCATION_CODE_FUNC_OFFSET
描述代码中函数中断点的偏移位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_FUNC_OFFSET {
    BSTR                     bstrContext;
    IDebugFunctionPosition2* pFuncPos;
} BP_LOCATION_CODE_FUNC_OFFSET;
```

## <a name="members"></a>成员
`bstrContext`\
断点的上下文，通常是调用堆栈上显示的方法或函数名称。

`pFuncPos`\
[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)对象，描述函数的名称以及函数开头的相对位置。

## <a name="remarks"></a>备注
此结构是 [联合BP_LOCATION结构](../../../extensibility/debugger/reference/bp-location.md) 的成员。

`pFuncPos`成员指示在何处设置函数断点。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)
