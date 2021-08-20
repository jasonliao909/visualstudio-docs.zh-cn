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
ms.openlocfilehash: d449a8d203f58eca3b892a31f8b1130d1c5f490a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103580"
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
