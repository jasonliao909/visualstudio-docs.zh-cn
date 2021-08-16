---
description: 用于根据用户可在集成开发环境中输入的字符串设置代码断点 (IDE) 。
title: BP_LOCATION_CODE_STRING |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_STRING
helpviewer_keywords:
- BP_LOCATION_CODE_STRING structure
ms.assetid: a4cd71c6-5052-45fe-907b-ebc6ca1df2e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
ms.openlocfilehash: 3ebfdd5605f3f332209d2030b499c70c12582d119d51cceef6f1014875bebe23
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342656"
---
# <a name="bp_location_code_string"></a>BP_LOCATION_CODE_STRING
用于根据用户可在集成开发环境中输入的字符串设置代码断点 (IDE) 。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION_CODE_STRING {
    BSTR bstrContext;
    BSTR bstrCodeExpr;
} BP_LOCATION_CODE_STRING;
```

## <a name="members"></a>成员
`bstrContext`\
代码内断点的上下文，通常是在调用堆栈上显示的方法或函数名称。

`bstrCodeExpr`\
用户键入的字符串，用于描述代码断点。

## <a name="remarks"></a>备注
此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
