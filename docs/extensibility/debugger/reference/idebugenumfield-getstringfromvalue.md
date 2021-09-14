---
description: 此方法根据枚举常量的值获取其名称。
title: IDebugEnumField：：GetStringFromValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 692d5fd16912be8645e99fd2b54a8fbb4871b007
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126665414"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
此方法根据枚举常量的值获取其名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetStringFromValue(
   ULONGLONG value,
   BSTR*     pbstrValue
);
```

```csharp
int GetStringFromValue(
   ulong      value,
   out string pbstrValue
);
```

## <a name="parameters"></a>parameters
`value`\
[in]要获取枚举常量的名称的值。

`pbstrValue`\
[out]返回枚举常量的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 ;否则，如果值没有关联名称，则返回 ; `S_OK` `S_FALSE` 否则返回错误代码。

## <a name="remarks"></a>备注
 如果多个名称与同一个值关联，则返回枚举中定义的名字。

## <a name="see-also"></a>另请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
