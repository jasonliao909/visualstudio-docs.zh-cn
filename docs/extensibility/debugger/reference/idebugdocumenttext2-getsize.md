---
description: 检索文档中此位置的文本大小。
title: IDebugDocumentText2：： GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 25fa2f9c4a36e292bf58c80cbfdb01c6ad021ce4
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602438"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
检索文档中此位置的文本大小。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   ULONG* pcNumLines,
   ULONG* pcNumChars
);
```

```csharp
int GetSize( 
   ref uint pcNumLines,
   ref uint pcNumChars
);
```

## <a name="parameters"></a>parameters
`pcNumLines`\
弄返回文本的行数。

`pcNumChars`\
弄返回文本的字符数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注

 [仅限 c + +]如果不需要特定值，则为参数传递 NULL。

 [仅限 c #]必须指定这两个参数。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
