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
ms.openlocfilehash: 4da6faf02b59ef8f004e2411d86b06f60c33020c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153012"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
允许查询有关目标计算机的信息。

## <a name="syntax"></a>语法

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 此接口由会话调试管理器的端口对象实现。

## <a name="methods"></a>方法
 下表显示的方法 `IDebugWindowsComputerPort2` 。

|方法|说明|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|检索有关正在运行调试器的计算机的信息。|

## <a name="requirements"></a>要求
 标头： Msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
