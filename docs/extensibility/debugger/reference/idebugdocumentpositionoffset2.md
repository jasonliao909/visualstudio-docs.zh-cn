---
title: IDebugDocumentPositionOffset2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2 interface
ms.assetid: f1b05db3-50d8-453f-a72f-e68b239236a4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 69fbdef70fc9c95ef571ce0ce796199292417ca0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933552"
---
# <a name="idebugdocumentpositionoffset2"></a>IDebugDocumentPositionOffset2
将源文件中的位置表示为字符偏移量。

## <a name="syntax"></a>语法

```
IDebugDocumentPositionOffset2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 由 IDE 实现并由调试引擎使用。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugDocumentPositionOffset2` 。

|方法|说明|
|------------|-----------------|
|[GetRange](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2-getrange.md)|检索当前文档位置的范围。|

## <a name="remarks"></a>备注
 这会返回与 [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md) 相同的信息，但会返回 `char` 文档开头的偏移量。 这会提供类似于磁盘上存在的文档，即一维字符数组，而不是通常返回的行和列信息。

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
