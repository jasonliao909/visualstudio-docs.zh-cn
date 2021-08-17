---
description: 检索源文件中给定位置的代码路径列表。
title: IDebugProgram2：：EnumCodePaths |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d5f04a988b7afae1b4b86c38e6fedba4c5d6d896
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122057468"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
检索源文件中给定位置的代码路径列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumCodePaths( 
   LPCOLESTR            pszHint,
   IDebugCodeContext2*  pStart,
   IDebugStackFrame2*   pFrame,
   BOOL                 fSource,
   IEnumCodePaths2**    ppEnum,
   IDebugCodeContext2** ppSafety
);
```

```csharp
int EnumCodePaths( 
   string                 pszHint,
   IDebugCodeContext2     pStart,
   IDebugStackFrame2      pFrame,
   Int                    fSource,
   out IEnumCodePaths2    ppEnum,
   out IDebugCodeContext2 ppSafety
);
```

## <a name="parameters"></a>参数
`pszHint`\
[in]IDE 中" **源"或** "反 **汇编"** 视图中光标下的单词。

`pStart`\
[in]表示 [当前代码上下文的 IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象。

`pFrame`\
[in]表示与当前断点关联的堆栈帧的 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) 对象。

`fSource`\
[in]如果在"源 () ，则不为零;如果在"反汇编"视图中 () 为 `TRUE`  `FALSE` **零。**

`ppEnum`\
[out]返回包含 [代码路径列表的 IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) 对象。

`ppSafety`\
[out]返回一 [个 IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 对象，该对象表示要设置为断点（如果跳过所选代码路径）的其他代码上下文。 例如，如果布尔表达式短路，则可能会发生这种情况。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 代码路径描述为到达程序执行中的当前点而调用的方法或函数的名称。 代码路径列表表示调用堆栈。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
