---
description: 表示"编辑并继续"不可用的原因。
title: EncUnavailableReason |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d14b48d4cc3e32c48886222919b5e1f80f72fc69
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160188"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!` 表示"编辑 **并继续"** 不可用的原因。

## <a name="syntax"></a>语法

```cpp
enum tagEncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
typedef enum tagEncUnavailableReason EncUnavailableReason;
```

```csharp
public enum EncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
```

## <a name="fields"></a>字段
`ENCUN_NONE`\
"编辑并继续"不可用的具体原因。

`ENCUN_INTEROP`\
在 InterOp 调用期间，"编辑并继续"不可用。

`ENCUN_SQLCLR`\
在使用公共语言运行时和 CLR SQL的调用过程中，"编辑并继续 (不可用) 。

`ENCUN_MINIDUMP`\
处理微型转储时，"编辑并继续"不可用。

`ENCUN_EMBEDDED`\
处理嵌入代码时，"编辑并继续"不可用。

`ENCUN_ATTACH`\
"编辑并继续"不可用，因为会话已附加到调试器，而不是由 调试器启动。

`ENCUN_WIN64`\
处理 64 位代码时，"编辑并继续Windows可用。

## <a name="remarks"></a>备注
此枚举仅供 内部使用 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。 由 [自定义端口供应商实现的 GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) 和 [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) 方法应始终返回 `E_NOTIMPL` 。

## <a name="requirements"></a>要求
标头：msdbg.idl

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
