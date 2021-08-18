---
description: 为调用 方法所需的每个参数的类型创建枚举器。
title: IDebugMethodField：：EnumArguments |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumArguments
helpviewer_keywords:
- IDebugMethodField::EnumArguments method
ms.assetid: 3ab55488-2437-4ff6-a9ae-78ea6d7b23a8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13ae620928aa3afce92ef12b43e3ac70f49a2467
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118614"
---
# <a name="idebugmethodfieldenumarguments"></a>IDebugMethodField::EnumArguments
为调用 方法所需的每个参数的类型创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumArguments( 
   IEnumDebugFields** ppParams
);
```

```csharp
int EnumArguments(
   out IEnumDebugFields ppParams
);
```

## <a name="parameters"></a>参数
`ppParams`\
[out]返回表示 [参数类型列表的 IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象。 如果没有参数，则返回 null 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK，如果没有参数S_FALSE则返回值。 否则，返回错误代码。

## <a name="remarks"></a>备注
 每个元素都是一个 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，表示每个参数的类型。 调用 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) 方法检索有关每个参数类型的信息。

 如果需要参数的名称以及 类型，请调用 [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [EnumParameters](../../../extensibility/debugger/reference/idebugmethodfield-enumparameters.md)
