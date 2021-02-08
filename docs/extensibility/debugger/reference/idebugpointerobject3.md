---
title: IDebugPointerObject3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPointerObject3 interface
ms.assetid: 11d26af4-1079-435e-96fa-d5269cbea8eb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0f4a87f9cf0bf64378e6dd5acba504d2da7b5d92
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844796"
---
# <a name="idebugpointerobject3"></a>IDebugPointerObject3
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 表示分析树中的指针，并扩展 **IDebugPointerObject** 接口。

## <a name="syntax"></a>语法

```
IDebugPointerObject3 : IDebugPointerObject
```

## <a name="notes-for-implementers"></a>实施者注意事项
 表达式计算器 (EE) 实现此接口。

## <a name="methods"></a>方法
 除了 [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetPointerAddress](../../../extensibility/debugger/reference/idebugpointerobject3-getpointeraddress.md)|检索指针的地址。|

## <a name="requirements"></a>要求
 标头： Ee。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll
