---
description: 按给定的语句或行数移动文档上下文。
title: IDebugDocumentContext2：： Seek |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2::Seek
helpviewer_keywords:
- IDebugDocumentContext2::Seek
ms.assetid: 71501356-8a82-4d36-b354-6625bdd2baa0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c9fcc430102ec974f2492a8e65894faa45978693
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066550"
---
# <a name="idebugdocumentcontext2seek"></a>IDebugDocumentContext2::Seek
按给定的语句或行数移动文档上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT Seek( 
   int                      nCount,
   IDebugDocumentContext2** ppDocContext
);
```

```cpp
int Seek( 
   int                        nCount,
   out IDebugDocumentContext2 ppDocContext
);
```

## <a name="parameters"></a>参数
`nCount`\
中要向前移动的语句或行数，具体取决于文档上下文。

`ppDocContext`\
弄返回一个新的 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 对象，该对象具有新位置。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
