---
description: 指定挂起断点和绑定断点的断点条件样式。
title: BP_COND_STYLE |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 750edd7dd48235acb4b2bc6e718999dd047ce36190a43a2468376c54beeddcd4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417777"
---
# <a name="bp_cond_style"></a>BP_COND_STYLE
指定挂起断点和绑定断点的断点条件样式。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="fields"></a>字段
`BP_COND_NONE`\
在到达断点的位置时触发断点。 未指定断点条件。

`BP_COND_WHEN_TRUE`\
仅在与断点关联的条件表达式计算结果为 时触发断点 `true` 。

`BP_COND_WHEN_CHANGED`\
仅在与断点关联的条件表达式的值与其以前的计算值发生更改时触发断点。

## <a name="remarks"></a>备注
用于 `styleCondition` 结构BP_CONDITION成员。 [](../../../extensibility/debugger/reference/bp-condition.md)

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
