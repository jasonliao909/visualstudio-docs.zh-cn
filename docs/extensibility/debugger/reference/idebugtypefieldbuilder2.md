---
description: 扩展 IDebugTypeFieldBuilder，以创建数组类型。
title: IDebugTypeFieldBuilder2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugTypeFieldBuilder2 interface
ms.assetid: 23911c5b-2bbf-4734-9976-87a0bd6ea36c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: c9484ea43bdb0343dff45359f150d32a0dc984591c548b64ce9d7f1279947db3
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121291852"
---
# <a name="idebugtypefieldbuilder2"></a>IDebugTypeFieldBuilder2
扩展 **IDebugTypeFieldBuilder，** 以创建数组类型。

## <a name="syntax"></a>语法

```
IDebugTypeFieldBuilder2 : IDebugTypeFieldBuilder
```

## <a name="notes-for-callers"></a>调用方说明
 可以从符号提供程序获取此接口。

## <a name="methods"></a>方法
 除了 [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[CreateArrayOfType](../../../extensibility/debugger/reference/idebugtypefieldbuilder2-createarrayoftype.md)|创建指定类型和大小的数组。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
