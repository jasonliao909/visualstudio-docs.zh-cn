---
description: 获取自定义属性附加到的字段。
title: IDebugCustomAttribute：：GetParentField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetParentField
helpviewer_keywords:
- IDebugCustomAttribute::GetParentField
ms.assetid: bcdfdf37-bfcf-4988-a7b8-4c731d0af1b0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f953a5d1d5f533468ff5de85553108cc988ca679
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111473"
---
# <a name="idebugcustomattributegetparentfield"></a>IDebugCustomAttribute::GetParentField
获取自定义属性附加到的字段。

## <a name="syntax"></a>语法

```cpp
HRESULT GetParentField( 
   IDebugField** ppField
);
```

```csharp
int GetParentField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
[out]返回 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象，该对象表示自定义属性附加到的字段。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 对返回的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象调用[GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)方法，以确定父级的字段类型。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
