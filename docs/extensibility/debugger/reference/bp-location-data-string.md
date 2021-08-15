---
description: 用于设置数据断点，这些断点基于用户可在集成开发环境中输入的字符串 (IDE) 。
title: BP_LOCATION_DATA_STRING |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_DATA_STRING
helpviewer_keywords:
- BP_LOCATION_DATA_STRING structure
ms.assetid: 445d6f3f-95b0-47ac-85e2-51b778240687
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 37495719a5590fff6dc2ec61cb863e2163f468c7ccf15e316a034cb510c4f0a5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121239329"
---
# <a name="bp_location_data_string"></a>BP_LOCATION_DATA_STRING
用于设置数据断点，这些断点基于用户可在集成开发环境中输入的字符串 (IDE) 。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_DATA_STRING {
    IDebugThread2* pThread;
    BSTR           bstrContext;
    BSTR           bstrDataExpr;
    DWORD          dwNumElements;
} BP_LOCATION_DATA_STRING;
```

## <a name="members"></a>成员
`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，它表示发生断点的线程。

`bstrContext`\
代码内断点的上下文，通常是在调用堆栈上显示的方法或函数名称。

`bstrDataExpr`\
用户输入的用于设置断点的数据字符串。

`dwNumElements`\
发生断点的数据字符串中的元素数。

## <a name="remarks"></a>备注
此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
