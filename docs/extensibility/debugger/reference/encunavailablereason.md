---
description: 表示 "编辑并继续" 不可用的原因。
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
ms.openlocfilehash: 5a47c29f07a590667a22ed123ba660202b4de9c449e606a8d921dd02eb0b7f52
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434394"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!` 表示 " **编辑并继续** " 不可用的原因。

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
"编辑并继续" 不可用的特定原因。

`ENCUN_INTEROP`\
在互操作调用期间，"编辑并继续" 不可用。

`ENCUN_SQLCLR`\
使用公共语言运行时 (CLR) 时，"编辑并继续" 不可 SQL 用。

`ENCUN_MINIDUMP`\
处理小型转储时，"编辑并继续" 不可用。

`ENCUN_EMBEDDED`\
在处理嵌入代码时，"编辑并继续" 不可用。

`ENCUN_ATTACH`\
"编辑并继续" 不可用，因为该会话已附加到调试器，而不是由调试器启动。

`ENCUN_WIN64`\
处理64位 Windows 代码时，"编辑并继续" 不可用。

## <a name="remarks"></a>备注
此枚举仅供内部使用 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 。 自定义端口供应商实现的 [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md) 和 [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md) 方法应始终返回 `E_NOTIMPL` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
