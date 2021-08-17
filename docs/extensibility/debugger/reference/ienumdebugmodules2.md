---
description: 此接口枚举模块列表。
title: IEnumDebugModules2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugModules2
helpviewer_keywords:
- IEnumDebugModules2
ms.assetid: 4fe28074-a960-41ad-b74d-b57f04c0c0ad
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 994d7d6a23638bfdeb78ba8807e5c6e6d19c39e7
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095369"
---
# <a name="ienumdebugmodules2"></a>IEnumDebugModules2
此接口枚举模块列表。

## <a name="syntax"></a>语法

```
IEnumDebugModules2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以表示为程序加载的模块的列表。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio 调用[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugModules2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)|检索枚举序列中指定数目的模块。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugmodules2-skip.md)|跳过枚举序列中指定数目的模块。|
|[重置](../../../extensibility/debugger/reference/ienumdebugmodules2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugmodules2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugmodules2-getcount.md)|获取模块的数目。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口主要用于更新 "**模块**" 窗口。

 为了在 Visual Studio 中进行调试，程序是可跨模块边界的代码指令的逻辑序列，因此需要单个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的模块列表。 列表中的第一个模块通常包含关联程序的初始入口点。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)
