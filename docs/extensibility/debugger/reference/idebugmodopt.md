---
description: 表示调试可选修饰符。
title: IDebugModOpt |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb235d58c254d130636da0f4b97961c11f9a372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087894"
---
# <a name="idebugmodopt"></a>IDebugModOpt
表示调试可选修饰符。

## <a name="syntax"></a>语法

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>调用方说明
 从表示类或方法的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象获取。

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|检索可选修饰符的列表。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
