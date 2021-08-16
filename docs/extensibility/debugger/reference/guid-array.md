---
description: 描述可用调试引擎的唯一标识符的数组。
title: GUID_ARRAY |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GUID_ARRAY structure
ms.assetid: 9e12500c-2c1c-49b1-a0ba-e08366c97eb8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0dc91c33672519a7bed0bc545179d91915ab38d1142728c2c614f6924548c411
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434264"
---
# <a name="guid_array"></a>GUID_ARRAY
描述可用调试引擎的唯一标识符的数组。

## <a name="syntax"></a>语法

```cpp
typedef struct tagGUID_ARRAY
{
    DWORD dwCount;
    GUID *Members;
} GUID_ARRAY;
```

```csharp
public struct GUID_ARRAY
{
    public uint dwCount;
    public Guid Members;
}
```

## <a name="members"></a>成员
`dwCount`\
数组中唯一标识符的数目。

`Members`\
包含唯一标识符的数组。

## <a name="remarks"></a>备注
此结构由 [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md) 方法返回。

## <a name="requirements"></a>要求
标头： Msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)
