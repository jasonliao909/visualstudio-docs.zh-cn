---
description: 此接口表示源文件中的抽象位置。
title: IDebugDocumentPosition2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentPosition2
helpviewer_keywords:
- IDebugDocumentPosition2 interface
ms.assetid: 0e838ced-12bb-4efc-b811-2b7c034b77b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 56e809bdc8b6cb8d22fc89cd216f9e8920dc4359
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119446"
---
# <a name="idebugdocumentposition2"></a>IDebugDocumentPosition2
此接口表示源文件中的抽象位置。

## <a name="syntax"></a>语法

```
IDebugDocumentPosition2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 Visual Studio实现此接口。 如果调试引擎 (DE) 必须像 DE 实现 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口一样提供自己的源代码， (也会实现此接口) 。

## <a name="notes-for-callers"></a>调用方说明
 此接口作为参数传递给 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)。 它还作为 BP_LOCATION 联合 (的[](../../../extensibility/debugger/reference/bp-location.md)一部分提供BP_LOCATION_CODE_FILE_LINE结构) ，该结构又属于[](../../../extensibility/debugger/reference/bp-location-code-file-line.md) [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)结构，用于创建挂起断点。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugDocumentPosition2` 。

|方法|说明|
|------------|-----------------|
|[GetFileName](../../../extensibility/debugger/reference/idebugdocumentposition2-getfilename.md)|获取包含此文档位置的源文件的文件名。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)|获取包含文档。|
|[IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)|确定此位置是否包含在给定文档中。|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)|获取此文档位置的范围。|

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
