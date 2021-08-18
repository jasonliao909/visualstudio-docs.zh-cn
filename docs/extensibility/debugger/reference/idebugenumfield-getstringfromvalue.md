---
description: 此方法获取给定其值的枚举常量的名称。
title: IDebugEnumField：： GetStringFromValue |Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122035093"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
此方法获取给定其值的枚举常量的名称。

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

## <a name="parameters"></a>参数
`value`\
中要为其获取枚举常量名称的值。

`pbstrValue`\
弄返回枚举常量的名称。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则， `S_FALSE` 如果值没有关联的名称，则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 如果有多个与同一值关联的名称，则将返回在枚举中定义的第一个名称。

## <a name="see-also"></a>请参阅
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
