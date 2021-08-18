---
description: 此方法将此字段与指定字段进行比较，实现相等性。
title: IDebugField：：Equal |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f9625aa138330f8504dd90371808a62f8c50ee9c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138453"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
此方法将此字段与指定字段进行比较，实现相等性。

## <a name="syntax"></a>语法

```cpp
HRESULT Equal( 
   IDebugField* pField
);
```

```csharp
int Equal(
   IDebugField pField
);
```

## <a name="parameters"></a>参数
`pField`\
[in]要与此字段进行比较的字段。

## <a name="return-value"></a>返回值
 如果字段相同，则 返回 `S_OK` 。 如果字段不同，则返回 `S_FALSE.` ;否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
