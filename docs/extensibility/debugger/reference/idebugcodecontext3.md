---
description: 扩展 IDebugCodeContext2 接口，以便能够检索模块和进程接口。
title: IDebugCodeContext3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugCodeContext3 interface
ms.assetid: 524eb882-0ad5-4bfb-95eb-eb3abb3d0237
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db806a4b45e855533e4ded1419f2d2117fb4f912
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164014"
---
# <a name="idebugcodecontext3"></a>IDebugCodeContext3
扩展 [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 接口，以便能够检索模块和进程接口。

## <a name="syntax"></a>语法

```
IDebugCodeContext3 : IDebugCodeContext2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 由调试引擎实现并由 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] 调试包使用。

## <a name="methods"></a>方法
 除了接口上的方法 `IDebugCodeContext2` ，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetModule](../../../extensibility/debugger/reference/idebugcodecontext3-getmodule.md)|检索对调试模块的接口的引用。|
|[GetProcess](../../../extensibility/debugger/reference/idebugcodecontext3-getprocess.md)|检索对调试进程的接口的引用。|

## <a name="remarks"></a>备注
 这是一个通常不需要实现的可选接口。

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
