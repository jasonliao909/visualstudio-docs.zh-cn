---
description: 表示托管代码泛型类型的字段的实例。
title: IDebugGenericFieldInstance |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugGenericFieldInstance interface
ms.assetid: f68b4761-be8b-4801-9d4b-cde90e01d95e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cf87999768ae12b9ae10702bc0e8ae8efe16e000
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105072749"
---
# <a name="idebuggenericfieldinstance"></a>IDebugGenericFieldInstance
表示托管代码泛型类型的字段的实例。

## <a name="syntax"></a>语法

```
IDebugGenericFieldInstance : IUnknown
```

## <a name="methods"></a>方法
 此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetTypeArguments](../../../extensibility/debugger/reference/idebuggenericfieldinstance-gettypearguments.md)|检索此实例的类型参数参数。|
|[TypeArgumentCount](../../../extensibility/debugger/reference/idebuggenericfieldinstance-typeargumentcount.md)|返回此实例的类型参数参数的数目。|

## <a name="requirements"></a>要求
 标头： Sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
