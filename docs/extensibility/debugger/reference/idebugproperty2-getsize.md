---
description: 获取属性值的大小（以字节为单位）。
title: IDebugProperty2：： GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetSize
helpviewer_keywords:
- IDebugProperty2::GetSize
ms.assetid: 0deb8ec5-d6fb-4622-bb14-0c46b9459cc6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7db319a420dc63eaec8afcdcbeaa38fe861a4bea
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064782"
---
# <a name="idebugproperty2getsize"></a>IDebugProperty2::GetSize
获取属性值的大小（以字节为单位）。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize ( 
   DWORD* pdwSize
);
```

```csharp
int GetSize ( 
   out uint pdwSize
);
```

## <a name="parameters"></a>参数
`pdwSize`\
弄返回属性值的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_GETSIZE_NO_SIZE`如果属性没有大小，则返回。

## <a name="see-also"></a>另请参阅
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
