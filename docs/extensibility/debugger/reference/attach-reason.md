---
description: 指定要附加到程序节点 (DE) 引擎的原因。
title: ATTACH_REASON |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ATTACH_REASON
helpviewer_keywords:
- ATTACH_REASON enumeration
ms.assetid: 159fb70b-a344-4ba6-9115-b7eaa16e228f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 185cec33a3ea8d6538ae6d820f0690bc68b5270daa74161d46f4788137b234e2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434485"
---
# <a name="attach_reason"></a>ATTACH_REASON
指定要附加到程序节点 (DE) 引擎的原因。

## <a name="syntax"></a>语法

```cpp
enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
typedef DWORD ATTACH_REASON;
```

```csharp
public enum enum_ATTACH_REASON {
    ATTACH_REASON_LAUNCH = 0x0001,
    ATTACH_REASON_USER   = 0x0002,
    ATTACH_REASON_AUTO   = 0x0003
};
```

## <a name="fields"></a>字段
`ATTACH_REASON_AUTO`\
附加，因为进程当前处于调试模式。

`ATTACH_REASON_LAUNCH`\
附加，因为进程已启动。

`ATTACH_REASON_USER`\
由于用户请求而附加。

## <a name="remarks"></a>备注
这些值用作 Attach 和 Attach[方法](../../../extensibility/debugger/reference/idebugengine2-attach.md)[的参数](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)
