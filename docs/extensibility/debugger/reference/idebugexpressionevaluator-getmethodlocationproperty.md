---
description: 此方法将方法位置和偏移量转换为内存地址。
title: IDebugExpressionEvaluator：： GetMethodLocationProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e5b520fc15d5cd1edff3331f4622c6086b3b58d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664519"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
此方法将方法位置和偏移量转换为内存地址。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMethodLocationProperty( 
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodLocationProperty(
   string               upstrFullyQualifiedMethodPlusOffset,
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>parameters
`upstrFullyQualifiedMethodPlusOffset`\
中表示为字符串的方法位置和偏移量。

`pSymbolProvider`\
中表示为 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 对象的符号提供程序。

`pAddress`\
中方法中的一个地址，以 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象的形式表示。

`pBinder`\
中表示为 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 对象的联编程序。

`ppProperty`\
弄返回表示内存地址的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 返回的地址可用于设置断点，例如。

 不管名称 `upstrFullyQualifiedMethodPlusOffset` 如何，都可以向此参数传递部分限定的方法名称。 在这种情况下，所选方法是括起来的方法 `pAddress` 。 如何解释此参数取决于表达式计算器的实现以及它所支持的语言。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
