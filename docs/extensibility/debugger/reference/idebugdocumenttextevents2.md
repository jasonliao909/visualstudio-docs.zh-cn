---
description: 此接口用于通知Visual Studio引擎提供的源文档的更改。
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
ms.openlocfilehash: 378dd2c8892b659f867f24f4a392cb6e099aeb477ab8044716ca0b99baddbc87
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121390211"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
此接口用于通知Visual Studio引擎提供的源文档的更改。

## <a name="syntax"></a>语法

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 实现此接口以支持对源代码进行更改。 此接口通常在实现 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) 接口的同一对象上实现。

## <a name="notes-for-callers"></a>调用方说明
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 通过对 方法的调用获取此 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> 接口。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>接口从对 方法的调用 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> 获取。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>通过调用[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)接口上的[QueryInterface](/cpp/atl/queryinterface)方法获取接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugDocumentTextEvents2` 。

|方法|说明|
|------------|-----------------|
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|指示整个文档已销毁。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|通知调试包已将文本插入到文档中。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|通知调试包已从文档中删除文本。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|通知调试包文档中已替换文本。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|通知调试包文档中的文本属性已更新。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|通知事件接收方文档属性已更新。|

## <a name="remarks"></a>备注
 只有提供自己的文档的调试引擎才能利用 `IDebugDocumentTextEvent2` 接口。 例如，脚本调试引擎。 在解释脚本的过程中，可以生成未存在于任何磁盘文件中且只有 DE 已知的新源代码。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
