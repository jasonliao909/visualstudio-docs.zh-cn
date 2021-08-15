---
description: 此方法获取有关 字段的可显示信息。
title: IDebugField：：GetInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetInfo
helpviewer_keywords:
- IDebugField::GetInfo method
ms.assetid: 7d508200-89ce-400f-a8ea-f28e7610cb2b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c41d00a8f8a42e3c92e88dec911b6d0fd638ecedd77665a240475b417da52072
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121389847"
---
# <a name="idebugfieldgetinfo"></a>IDebugField::GetInfo
此方法获取有关 字段的可显示信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo( 
   FIELD_INFO_FIELDS dwFields,
   FIELD_INFO* pFieldInfo
);
```

```csharp
int GetInfo(
   enum_FIELD_INFO_FIELDS dwFields,
   FIELD_INFO[] pFieldInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
[in]一个 [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md) 常量的组合，用于选择要显示的信息。 如果字段表示符号，则这通常是符号名称和类型。

`pFieldInfo`\
[out]返回所提供的结构[FIELD_INFO信息。](../../../extensibility/debugger/reference/field-info.md)

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
