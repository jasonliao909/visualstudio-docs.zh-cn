---
description: 此接口表示文本文档。
title: IDebugDocumentText2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 4ffa88c04333243ba016477e98a216bf957616ab
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119407"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
此接口表示文本文档。

## <a name="syntax"></a>语法

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 在需要提供源代码时以文本形式实现此接口。 由于这是最典型的情况，如果 DE 实现 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口，则它还应实现 `IDebugDocumentText2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 使用 `QueryInterface` 方法从接口获取此 `IDebugDocument2` 接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 接口上的方法 `IDebugDocument2` 外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|检索文档中此位置的文本大小。|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|从文档中的指定位置检索文本。|

## <a name="remarks"></a>备注
 实现此接口的对象还必须实现 接口，该接口 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 为 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) 对象提供 接口。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
