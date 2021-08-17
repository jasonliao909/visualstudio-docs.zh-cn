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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 5211ad750391c8f7f43eb5a7084c090ff26c8d45
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122137894"
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
