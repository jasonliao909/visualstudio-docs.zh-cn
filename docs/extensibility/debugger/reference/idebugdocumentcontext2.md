---
description: 此接口表示源文件文档中的位置。
title: IDebugDocumentContext2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: b28f18061f6a0bc76ad69da6a2fc27b0d30593f6
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602449"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
此接口表示源文件文档中的位置。

## <a name="syntax"></a>语法

```
IDebugDocumentContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口，作为对源代码级调试的支持的一部分。 除了源代码中的位置，此接口还提供用于比较上下文和浏览源代码文档的方法。

## <a name="notes-for-callers"></a>调用方说明
 多个接口上的方法（通常是 [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) 和 [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) 接口）返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugDocumentContext2` 。

|方法|说明|
|------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|获取包含此文档上下文的文档。|
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|获取包含此文档上下文的文档的可显示名称。|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|检索与此文档上下文关联的所有代码上下文的列表。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|获取与此文档上下文关联的语言。|
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|获取此文档上下文的文件语句范围。|
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|获取此文档上下文的文件源范围。|
|[比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|将此文档上下文与给定的文档上下文数组进行比较。|
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|按给定数量的语句或行移动文档上下文。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
