---
description: 此接口枚举当前调试会话中正在运行的程序。
title: IEnumDebugPrograms2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPrograms2
helpviewer_keywords:
- IEnumDebugPrograms2
ms.assetid: 7fbb8fb7-db64-4546-a364-dc668430c8af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 3ff57a503094e018e65bdf9913c48cb3abc9f9c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664410"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
此接口枚举当前调试会话中正在运行的程序。

## <a name="syntax"></a>语法

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口，以提供由 DE 调试的程序列表。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio 调用[EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)以获取此接口。 Visual Studio 不使用[EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md) 。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugPrograms2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|检索枚举序列中指定数量的程序。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|跳过枚举序列中指定数量的程序。|
|[重置](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|获取枚举器中的程序数。|

## <a name="remarks"></a>备注
 Visual Studio 使用此接口来执行以下操作：

- 通过调用 [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)并在每个程序) 上调用 [EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)来填充 "**模块**" 窗口 (。

- 通过调用 `IDebugProcess2::EnumPrograms` 并在每个[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口上调用[QueryInterface](/cpp/atl/queryinterface)来填充 "附加到进程" 列表 (，以获取[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)接口) 。

- 生成一个 DEs 列表，以使用 [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)) 在进程 (调试每个程序。

- 通过调用 IDebugProcess2：： EnumPrograms 并调用 [GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)) ，将 "编辑并继续" (ENC 应用于每个程序 (的更新) 更新。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
