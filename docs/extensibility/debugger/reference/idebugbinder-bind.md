---
description: 此方法获取包含符号的当前值的内存上下文或对象。
title: IDebugBinder：：Bind |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::Bind
helpviewer_keywords:
- IDebugBinder::Bind method
ms.assetid: 15a11ad7-0fcc-4e80-ae34-8a7dd7bae3c3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: de3cbb35245fad317014136177a4a410edfb25b5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126600923"
---
# <a name="idebugbinderbind"></a>IDebugBinder::Bind
此方法获取包含符号的当前值的内存上下文或对象。

## <a name="syntax"></a>语法

```cpp
HRESULT Bind( 
   IDebugObject*  pContainer,
   IDebugField*   pField,
   IDebugObject** ppObject
);
```

```csharp
int Bind(
   IDebugObject     pContainer,
   IDebugField      pField,
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>parameters
`pContainer`\
[in]包含[引用的子项的 IDebugObject。](../../../extensibility/debugger/reference/idebugobject.md) `pField`

`pField`\
[in]表示[符号的 IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

`ppObject`\
[out]返回 `IDebugObject` 表示符号实例的 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
