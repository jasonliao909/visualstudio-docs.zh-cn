---
description: 表示托管代码泛型类型的参数。
title: IDebugGenericParamField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField interface
ms.assetid: ba24f499-5ba7-4c67-83e6-923229b52327
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
ms.openlocfilehash: 6960983be5b71162f95a0fcbd5a3152ee4c7362d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664495"
---
# <a name="idebuggenericparamfield"></a>IDebugGenericParamField
表示托管代码泛型类型的参数。

## <a name="syntax"></a>语法

```
IDebugGenericParamField : IDebugField
```

## <a name="notes-for-implementers"></a>实现者说明
 用于支持泛型。

## <a name="methods"></a>方法
 除了 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 接口上的方法外，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[ConstraintCount](../../../extensibility/debugger/reference/idebuggenericparamfield-constraintcount.md)|返回与此泛型参数关联的约束数。|
|[GetConstraints](../../../extensibility/debugger/reference/idebuggenericparamfield-getconstraints.md)|检索与此泛型参数关联的约束。|
|[GetFlags](../../../extensibility/debugger/reference/idebuggenericparamfield-getflags.md)|检索此泛型参数的标志。|
|[GetIndex](../../../extensibility/debugger/reference/idebuggenericparamfield-getindex.md)|检索此泛型参数的索引。|
|[GetNameOfFormalParam](../../../extensibility/debugger/reference/idebuggenericparamfield-getnameofformalparam.md)|检索此泛型参数的名称。|
|[GetOwner](../../../extensibility/debugger/reference/idebuggenericparamfield-getowner.md)|检索此泛型参数的类型或方法所有者。|

## <a name="requirements"></a>要求
 标头：Sh.h

 命名空间：Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll
