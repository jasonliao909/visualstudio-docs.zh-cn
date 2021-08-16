---
description: 如果任何可能支持此对象所表示的属性的) ，则获取字段或变量 (。
title: IDebugObject2：： GetBackingFieldForProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0019f890f8f487d455e92854f812296fa7dffd94fdde62c13505db2ba69bfe4f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339276"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
如果任何可能支持此对象所表示的属性的) ，则获取字段或变量 (。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
弄描述支持字段的 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)对象表示托管代码类属性，即具有 get 和/或 set 访问器的方法。 此类属性通常需要一个变量来包含属性操作的值。 此变量称为支持字段。 如果该对象没有支持字段，则确保返回空值：某些调用方可能不会注意到返回值，而是查看中是否返回了 null 值 `ppObject` 。

## <a name="see-also"></a>另请参阅
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
