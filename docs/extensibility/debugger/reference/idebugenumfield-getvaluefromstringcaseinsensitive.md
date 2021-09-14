---
description: 此方法使用不区分大小写的搜索来返回与枚举常量名称关联的值。
title: IDebugEnumField：： GetValueFromStringCaseInsensitive |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a39bb6ae031aac8ae9fb72134ff3744dacb59ece
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602428"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
此方法使用不区分大小写的搜索来返回与枚举常量名称关联的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetValueFromStringCaseInsensitive(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromStringCaseInsensitive(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>parameters
`pszValue`\
中一个字符串，指定要获取其值的名称。 请注意，对于 c + +，这是宽字符字符串。

`pValue`\
弄返回关联的数值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ; 否则， `S_FALSE` 如果该名称不是枚举的一部分，则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不区分大小写。 如果需要区分大小写的搜索 (例如，使用 c + + （其中名称区分大小写) ），请使用 [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)。

## <a name="see-also"></a>另请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
