---
description: 此接口枚举在当前调试会话中运行的程序。
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122034794"
---
# <a name="ienumdebugprograms2"></a>IEnumDebugPrograms2
此接口枚举在当前调试会话中运行的程序。

## <a name="syntax"></a>语法

```
IEnumDebugPrograms2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 调试引擎 (DE) 实现此接口以提供 DE 正在调试的程序的列表。

## <a name="notes-for-callers"></a>调用方说明
 Visual Studio [EnumPrograms 来获取](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)此接口。 [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)不由Visual Studio。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IEnumDebugPrograms2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugprograms2-next.md)|检索枚举序列中指定数量的程序。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugprograms2-skip.md)|跳过枚举序列中的指定数量的程序。|
|[重置](../../../extensibility/debugger/reference/ienumdebugprograms2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugprograms2-clone.md)|创建一个枚举器，其中包含与当前枚举器相同的枚举状态。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugprograms2-getcount.md)|获取枚举器中的程序数。|

## <a name="remarks"></a>备注
 Visual Studio使用此接口来：

- 通过调用 [EnumPrograms，](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)然后在每个程序 (调用[EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)来填充"模块") 。

- 通过在每个 `IDebugProcess2::EnumPrograms` [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口上 ([QueryInterface](/cpp/atl/queryinterface)来获取[IDebugEngineProgram2](../../../extensibility/debugger/reference/idebugengineprogram2.md)接口，以填充"附加到进程"列表) 。

- 生成可以使用 [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) (调试进程中每个程序的 DES) 。

- 通过调用 IDebugProcess2：：EnumPrograms，然后调用 [GetENCUpdate](../../../extensibility/debugger/reference/idebugprogram2-getencupdate.md)) ，将"编辑并继续" ( (ENC) 更新应用到每个程序。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugengine2-enumprograms.md)
- [EnumPrograms](../../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)
