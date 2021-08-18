---
description: 由事件处理程序调用，用于检索有关符号加载进程的结果。
title: IDebugSymbolSearchEvent2：：GetSymbolSearchInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
helpviewer_keywords:
- IDebugSymbolSearchEvent2::GetSymbolSearchInfo
ms.assetid: ae9eb72b-f2aa-43b8-87ca-da19d2e78d17
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1ccf00b144da55323281db33a1ee23814d212a79
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122070918"
---
# <a name="idebugsymbolsearchevent2getsymbolsearchinfo"></a>IDebugSymbolSearchEvent2::GetSymbolSearchInfo
由事件处理程序调用，用于检索有关符号加载进程的结果。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSymbolSearchInfo(
   IDebugModule3**    pModule,
   BSTR*              pbstrDebugMessage,
   MODULE_INFO_FLAGS* pdwModuleInfoFlags
);
```

```csharp
int GetSymbolSearchInfo(
   IDebugModule3              pModule,
   ref string                 pbstrDebugMessage,
   out enum_MODULE_INFO_FLAGS pdwModuleInfoFlags
);
```

## <a name="parameters"></a>参数
`pModule`\
[out]一个 IDebugModule3 对象，表示已加载符号的模块。

`pbstrDebugMessage`\
[in， out]返回一个字符串，其中包含模块的任何错误消息。 如果没有错误，则此字符串将仅包含模块的名称，但它永远不会为空。

> [!NOTE]
> [C++] `pbstrDebugMessage` 不能为 `NULL` ，并且必须使用 释放 `SysFreeString` 。

`pdwModuleInfoFlags`\
[out]来自 MODULE_INFO_FLAGS [标志的组合](../../../extensibility/debugger/reference/module-info-flags.md) ，指示是否加载了任何符号。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当处理程序在尝试加载模块的调试符号后收到 [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md) 事件时，处理程序可以调用 thismethod 来确定该加载的结果。

## <a name="see-also"></a>请参阅
- [IDebugModule3](../../../extensibility/debugger/reference/idebugmodule3.md)
- [MODULE_INFO_FLAGS](../../../extensibility/debugger/reference/module-info-flags.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
