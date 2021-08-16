---
description: 此方法将此字段与指定的字段进行比较以确定是否相等。
title: IDebugField：：等于 |Microsoft Docs
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
ms.openlocfilehash: 8bd276433883b833a56654357cdb4dc8695f79604a11d3e65836b1dc0e10d2bb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433900"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
此方法将此字段与指定的字段进行比较以确定是否相等。

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
中要与此进行比较的字段。

## <a name="return-value"></a>返回值
 如果字段相同，则返回 `S_OK` 。 如果字段不同，则返回 `S_FALSE.` ，否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
