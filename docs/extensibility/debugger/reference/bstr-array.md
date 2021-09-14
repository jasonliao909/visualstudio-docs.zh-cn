---
description: 描述字符串数组的 结构。
title: BSTR_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BSTR_ARRAY
helpviewer_keywords:
- BSTR_ARRAY structure
ms.assetid: 48da37f7-a237-48a9-9ff9-389c1a00862c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 43a4b68824b613cb0701ea5ccfb3ed334f715b69
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602490"
---
# <a name="bstr_array"></a>BSTR_ARRAY
描述字符串数组的 结构。

## <a name="syntax"></a>语法

```cpp
typedef struct tagBSTR_ARRAY {
    DWORD dwCount;
    BSTR* Members;
} BSTR_ARRAY;
```

```csharp
struct BSTR_ARRAY {
    DWORD    dwCount;
    string[] Members;
}
```

## <a name="members"></a>成员
`dwCount`\
数组中的字符串 `Members` 数。

`Members`\
字符串数组。

## <a name="remarks"></a>备注
此结构从 [EnumPersistedPorts 方法](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md) 返回。

 [仅 C++]必须使用 释放每个单个字符串 `SysFreeString` ， `Members` 并且必须使用 释放数组 `CoTaskMemFree` 。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [EnumPersistedPorts](../../../extensibility/debugger/reference/idebugportsupplier3-enumpersistedports.md)
