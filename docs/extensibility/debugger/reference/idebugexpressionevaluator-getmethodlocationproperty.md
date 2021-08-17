---
description: 此方法将方法位置和偏移量转换为内存地址。
title: IDebugExpressionEvaluator：：GetMethodLocationProperty |Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096175"
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

## <a name="parameters"></a>参数
`upstrFullyQualifiedMethodPlusOffset`\
[in]方法位置和偏移量，以字符串形式表示。

`pSymbolProvider`\
[in]表示为 [IDebugSymbolProvider 对象的符号](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 提供程序。

`pAddress`\
[in]方法中的地址，以 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象表示。

`pBinder`\
[in]表示为 [IDebugBinder 对象的](../../../extensibility/debugger/reference/idebugbinder.md) 联编程序。

`ppProperty`\
[out]返回表示 [内存地址的 IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 例如，返回的地址可用于设置断点。

 尽管名称 `upstrFullyQualifiedMethodPlusOffset` 为 ，但此参数可以传递部分限定的方法名称。 在这种情况下，所选方法是包含 的方法 `pAddress` 。 此参数的解释方式由表达式计算程序及其支持的语言的实现决定。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
