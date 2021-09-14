---
description: 获取描述此事件位置的文档上下文。
title: IDebugCanStopEvent2：： GetDocumentContext |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetDocumentContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetDocumentContext
ms.assetid: 936a6c4e-30c5-4c7e-9ad5-910cc605a4b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 24c7bb7d2dbbc5b9f1bd6c27980a755a5202a840
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602628"
---
# <a name="idebugcanstopevent2getdocumentcontext"></a>IDebugCanStopEvent2::GetDocumentContext
获取描述此事件位置的文档上下文。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDocumentContext ( 
   IDebugDocumentContext2** ppDocCxt
);
```

```csharp
int GetDocumentContext ( 
   out IDebugDocumentContext2 ppDocCxt
);
```

## <a name="parameters"></a>parameters
`ppDocCxt`\
弄返回 [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) 接口，该接口表示源文件文档中与当前代码位置对应的位置。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通常，可以将文档上下文视为源文件中的位置。

 若要获取面向代码说明的代码上下文，请调用 [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
