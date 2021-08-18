---
description: 此方法返回此指针对象指向的对象的类型。
title: IDebugPointerField：：GetDereferencedField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 70ceab57784de916b9f6941e97f70d65d3d7826e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088362"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
此方法返回此指针对象指向的对象的类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetDereferencedField(
   IDebugField** ppField
);
```

```csharp
int GetDereferencedField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`ppField`\
[out]返回[描述目标对象的类型的 IDebugField。](../../../extensibility/debugger/reference/idebugfield.md)

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 例如，如果 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) 对象指向整数，则此方法返回的 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 类型将描述该整数类型。

## <a name="see-also"></a>请参阅
- [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
