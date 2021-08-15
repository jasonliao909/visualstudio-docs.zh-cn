---
description: 从连续的字节序列中设置对象的值。
title: IDebugObject：： SetValue |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8469773cf57d8cac2c24f04260a6d1037de125b2691115b270a3b0c693cd675b
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339289"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
从连续的字节序列中设置对象的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int SetValue(
   byte[] pValue,
   uint   nSize
);
```

## <a name="parameters"></a>参数
`pValue`\
中表示新值的字节数组。

`nSize`\
中值的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 数组中的值将复制到此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象中，并替换任何现有值。 新值的大小可以大于或小于现有值。 此 `IDebugObject` 值不能为 null 引用。

## <a name="see-also"></a>另请参阅
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
