---
description: 允许查询有关目标计算机的信息。
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 43eb5a549fe4713a5746ada29938eeba850e49d414484fa269269b7682a16c3a
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121448698"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
允许查询有关目标计算机的信息。

## <a name="syntax"></a>语法

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实现者说明
 此接口由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示了 的方法 `IDebugWindowsComputerPort2` 。

|方法|说明|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|检索有关运行调试器的计算机的信息。|

## <a name="requirements"></a>要求
 标头：Msdbg.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
