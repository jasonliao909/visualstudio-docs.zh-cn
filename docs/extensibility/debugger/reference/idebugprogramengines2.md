---
description: 此接口由程序节点用来指定可调试此 (DE) 的所有可能的调试引擎。
title: IDebugProgramEngines2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2
helpviewer_keywords:
- IDebugProgramEngines2 interface
ms.assetid: 53d648f0-6c11-4337-badd-c43f3872b62c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: eedc4dd60ce3fbd8581e91ee14404abbe6454a62
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126409"
---
# <a name="idebugprogramengines2"></a>IDebugProgramEngines2
此接口由程序节点用来指定可调试此 (DE) 的所有可能的调试引擎。

## <a name="syntax"></a>语法

```
IDebugProgramEngines2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 DE 或自定义端口供应商在实现 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 的同一对象上实现此接口，以支持建立用于特定程序的特定 DE。

## <a name="notes-for-callers"></a>调用方说明
 在 [接口上调用 QueryInterface](/cpp/atl/queryinterface) `IDebugProgramNode2` 以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法 `IDebugProgramEngines2` 。

|方法|说明|
|------------|-----------------|
|[EnumPossibleEngines](../../../extensibility/debugger/reference/idebugprogramengines2-enumpossibleengines.md)|指示可以调试此程序的所有可能的 DES。|
|[SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)|选择要用于调试此程序的 DE。|

## <a name="remarks"></a>备注
 用户选择 DE 后，通过调用 [SetEngine](../../../extensibility/debugger/reference/idebugprogramengines2-setengine.md)向程序节点注册该选择。 所选引擎将成为 [GetEngineInfo 返回的引擎](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)。

## <a name="requirements"></a>要求
 标头：msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)
