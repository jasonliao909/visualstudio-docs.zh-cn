---
description: 此接口用于通知 Visual Studio 对调试引擎提供的源文档所做的更改。
title: IDebugDocumentTextEvents2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 1a90cd9ae5fa9e43a12a7b023f807aaf16ceef58
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122119199"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
此接口用于通知 Visual Studio 对调试引擎提供的源文档所做的更改。

## <a name="syntax"></a>语法

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 DE 实现此接口以支持对源代码进行更改。 此接口通常在实现 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口的同一对象上实现。

## <a name="notes-for-callers"></a>调用方说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 通过调用方法获取此接口 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> 。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>接口是通过调用方法获取的 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> 。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>接口是通过在[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)方法获取的。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IDebugDocumentTextEvents2` 。

|方法|说明|
|------------|-----------------|
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|指示整个文档已销毁。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|通知调试包文本已插入到文档中。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|通知调试包文本已从文档中删除。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|通知调试包文本已在文档中被替换。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|通知调试包文本属性已在文档中更新。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|通知接收方事件已更新文档属性。|

## <a name="remarks"></a>备注
 只有提供自己的文档的调试引擎才能利用 `IDebugDocumentTextEvent2` 界面。 这种情况的一个示例就是脚本调试引擎。 在解释脚本的过程中，可能会生成不存在于任何磁盘文件中的新源代码，并且只有取消。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
