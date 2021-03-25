---
description: 表示 IDebugBinder 对象的动态字段。
title: IDebugDynamicFieldCOMPlus |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDynamicFieldCOMPlus interface
ms.assetid: c3a25f27-327a-4bdb-b026-27d436ddcd0c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f365bcadba5349ae43e1b75683ec100fdabbf338
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094011"
---
# <a name="idebugdynamicfieldcomplus"></a>IDebugDynamicFieldCOMPlus
表示 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 对象的动态字段。

## <a name="syntax"></a>语法

```
IDebugDynamicFieldCOMPlus : IDebugDynamicField
```

## <a name="methods"></a>方法
 除了 [IDebugDynamicField](../../../extensibility/debugger/reference/idebugdynamicfield.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetTypeFromPrimitive](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromprimitive.md)|根据给定的基元类型检索类型。|
|[GetTypeFromTypeDef](../../../extensibility/debugger/reference/idebugdynamicfieldcomplus-gettypefromtypedef.md)|在给定其标记的情况中检索类型。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
