---
description: 获取此文档上下文的源代码范围。
title: IDebugDocumentContext2：：GetSourceRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::GetSourceRange
helpviewer_keywords:
- IDebugDocumentContext2::GetSourceRange
ms.assetid: 5903c75e-5390-4d13-9314-1ee276255313
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0eeec0f04f45cda0c257299923f0da9224312974
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602455"
---
# <a name="idebugdocumentcontext2getsourcerange"></a>IDebugDocumentContext2::GetSourceRange
获取此文档上下文的源代码范围。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSourceRange( 
   TEXT_POSITION* pBegPosition,
   TEXT_POSITION* pEndPosition
);
```

```csharp
int GetSourceRange( 
   TEXT_POSITION[] pBegPosition,
   TEXT_POSITION[] pEndPosition
);
```

## <a name="parameters"></a>parameters
`pBegPosition`\
[in， out]一 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 一个结构，该结构用起始位置填充。 如果不需要此信息，则此参数设置为 null 值。

`pEndPosition`\
[in， out]用 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 填充的一个结构。 如果不需要此信息，则此参数设置为 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 源范围是源代码的整个范围，从当前语句返回到提供代码的上一语句之后。 源范围通常用于将源语句（包括注释）与反汇编窗口中的代码混合使用。

 若要仅获取此文档上下文中包含的代码语句的范围，请调用 [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
