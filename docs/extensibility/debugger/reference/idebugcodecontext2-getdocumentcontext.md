---
description: 获取与此代码上下文相对应的文档上下文。
title: IDebugCodeContext2：： GetDocumentContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2::GetDocumentContext
helpviewer_keywords:
- IDebugCodeContext2::GetDocumentContext
ms.assetid: d552cc92-963f-43c1-949f-ae6b63a427b8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9aadc89257d86bac9432026d368c1f84e963152a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122079826"
---
# <a name="idebugcodecontext2getdocumentcontext"></a>IDebugCodeContext2::GetDocumentContext
获取与此代码上下文相对应的文档上下文。 文档上下文表示源文件中的一个位置，该位置对应于生成此指令的源代码。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDocumentContext( 
   IDebugDocumentContext2** ppSrcCxt
);
```

```csharp
int GetDocumentContext( 
   out IDebugDocumentContext2 ppSrcCxt
);
```

## <a name="parameters"></a>参数
`ppSrcCxt`\
弄返回对应于代码上下文的 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 对象。 如果 `S_OK` 返回，则数列应为非 `null` 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_FAIL`当参数为时（如 `out` `null` 代码上下文没有关联的源位置时），调试引擎应返回失败代码，如。

## <a name="remarks"></a>备注
 通常，可以将文档上下文视为源文件中的一个位置，而代码上下文是代码指令在执行流中的位置。

## <a name="see-also"></a>请参阅
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
