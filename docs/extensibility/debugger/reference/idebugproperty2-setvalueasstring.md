---
description: 设置给定字符串的属性的值。
title: IDebugProperty2：： SetValueAsString |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6d71f6926e9b973f83ae8f6d8e4a64ac127eaca6cf85e335cb6970c261c56840
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121449009"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
设置给定字符串的属性的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValueAsString ( 
   LPCOLESTR pszValue,
   UINT      nRadix,
   DWORD     dwTimeout
);
```

```csharp
int SetValueAsString ( 
   string pszValue,
   uint   nRadix,
   uint   dwTimeout
);
```

## <a name="parameters"></a>参数
`pszValue`\
中包含要设置的值的字符串。

`nRadix`\
中用于解释任何数值信息的基数。 这可以是0，尝试自动确定基数。

`dwTimeout`\
中指定从此方法返回之前要等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了其他可能的值。

|值|说明|
|-----------|-----------------|
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法将该字符串转换为属性值，或者无法设置该属性的值。|
|`E_SETVALUE_VALUE_IS_READONLY`|属性为只读属性。|

## <a name="see-also"></a>请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
