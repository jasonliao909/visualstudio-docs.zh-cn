---
description: 此方法返回与枚举常量的名称关联的值。
title: IDebugEnumField：：GetValueFromString |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromString
helpviewer_keywords:
- IDebugEnumField::GetValueFromString method
ms.assetid: 1ef8ac5e-a3e0-4078-b876-7f5615aedcbb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3060fafd2c887dd79933bb1baa04644d77a1113a132c3d751b31332c7643d526
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121360503"
---
# <a name="idebugenumfieldgetvaluefromstring"></a>IDebugEnumField::GetValueFromString
此方法返回与枚举常量的名称关联的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValueFromString(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromString(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>参数
`pszValue`\
[in]一个字符串，指定要获取其值的名称。 请注意，对于 C++，这是一个宽字符串。

`pValue`\
[out]返回关联的数值。

## <a name="return-value"></a>返回值
 如果成功，则返回 ;否则，如果名称不是枚举的一部分，则返回 `S_OK` `S_FALSE` ，否则返回错误代码。

## <a name="remarks"></a>备注
 此方法区分大小写。 如果需要不区分大小写的 (例如，在名称不区分大小写的 Visual Basic 等语言中，) [GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)。

## <a name="see-also"></a>另请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)
