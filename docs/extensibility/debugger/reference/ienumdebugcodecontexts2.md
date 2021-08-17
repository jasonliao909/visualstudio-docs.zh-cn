---
description: 此接口枚举与调试会话或特定程序或文档关联的代码上下文。
title: IEnumDebugCodeContexts2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2
helpviewer_keywords:
- IEnumDebugCodeContexts2
ms.assetid: 72915146-215f-4c99-a034-131b2b474e0e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 8b52be981dbda8bb3b73fc2596dc8988e021765d
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095616"
---
# <a name="ienumdebugcodecontexts2"></a>IEnumDebugCodeContexts2
此接口枚举与调试会话或特定程序或文档关联的代码上下文。

## <a name="syntax"></a>语法

```
IEnumDebugCodeContexts2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口来表示程序中特定文本位置的代码上下文列表或特定文档上下文的代码上下文列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md) 以获取此接口，该接口表示程序源文档中特定文本位置的代码上下文列表。

 调用 [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md) 以获取此接口，该接口表示特定源文档中所有代码上下文的列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IEnumDebugCodeContexts2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)|检索枚举序列中指定数目的代码上下文。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-skip.md)|跳过枚举序列中指定数目的代码上下文。|
|[重置](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-getcount.md)|获取枚举器中的代码上下文数。|

## <a name="remarks"></a>备注
 Visual Studio [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)以填充用户在设置下一语句或显示源文件的反汇编时可以选择的代码上下文列表。 例如，当 C++样式模板有多个实例时，可能会出现多个代码上下文。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugprogram2-enumcodecontexts.md)
- [EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)
