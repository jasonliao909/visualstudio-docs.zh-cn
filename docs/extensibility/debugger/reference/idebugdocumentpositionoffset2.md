---
description: 将源文件中的位置表示为字符偏移量。
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: f6fdb3fc220a4495146ad9ca66e4b2cee73f1909
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119432"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
将源文件中的位置表示为字符偏移量。

## <a name="syntax"></a>语法

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 由 IDE 实现，由调试引擎使用。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugDocumentPositionOffset2` 。

|方法|说明|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|检索当前文档位置的范围。|

## <a name="remarks"></a>备注
 这会返回与 [GetRange 相同的信息](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md) ，但 `char` 与文档开头的偏移量相同。 这会像在磁盘上（即一维字符数组）一样呈现文档，而不是通常返回的行和列信息。

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
