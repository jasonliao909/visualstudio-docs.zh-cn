---
description: 描述代码中某个地址处的断点位置。
title: BP_LOCATION_CODE_ADDRESS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 961a62284b841d56ae73a29df0e83810ff9d7d20
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102144437"
---
# <a name="bp_location_code_address"></a>BP_LOCATION_CODE_ADDRESS
描述代码中某个地址处的断点位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_ADDRESS {
    BSTR bstrContext;
    BSTR bstrModuleUrl;
    BSTR bstrFunction;
    BSTR bstrAddress;
} BP_LOCATION_CODE_ADDRESS;
```

## <a name="members"></a>成员
`bstrContext`\
断点的上下文，通常是在调用堆栈上显示的方法或函数名称。

`bstrModuleUrl`\
包含断点的模块的 URL。

`bstrFunction`\
包含断点的函数的名称。

`bstrAddress`\
断点的地址，表达式计算器会分析该地址，以将其绑定到 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象。

## <a name="remarks"></a>备注
此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
