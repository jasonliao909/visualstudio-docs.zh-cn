---
description: 此接口表示一个文本文档。
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
ms.openlocfilehash: ffb2aa817caff01b598bc789c6aaa8b7dbacfcd1d3d590a7715f6be4e18d1121
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121417335"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
此接口表示一个文本文档。

## <a name="syntax"></a>语法

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 在其需要提供的源代码采用文本格式时实现此接口。 由于这是最典型的情况，因此，如果 DE 实现了 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口，则它还应该实现 `IDebugDocumentText2` 接口。

## <a name="notes-for-callers"></a>调用方说明
 使用 `QueryInterface` 方法可从接口获取此接口 `IDebugDocument2` 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了接口上的方法 `IDebugDocument2` ，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|检索文档中此位置的文本大小。|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|从文档中的指定位置检索文本。|

## <a name="remarks"></a>备注
 实现此接口的对象还必须实现 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 接口，该接口提供 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) 对象的接口。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
