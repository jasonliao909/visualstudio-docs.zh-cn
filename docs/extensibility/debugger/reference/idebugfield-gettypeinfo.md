---
description: 此方法获取有关符号或类型的与类型无关的信息。
title: IDebugField：：GetTypeInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetTypeInfo
helpviewer_keywords:
- IDebugField::GetTypeInfo method
ms.assetid: bb5acfa3-04c3-4088-be84-9ff8926cd16f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8403a6eca0be5089d448c938720981b59862b404
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122138362"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
此方法获取有关符号或类型的与类型无关的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeInfo( 
   TYPE_INFO* pTypeInfo
);
```

```csharp
int GetTypeInfo(
   TYPE_INFO[] pTypeInfo
);
```

## <a name="parameters"></a>参数
`pTypeInfo`\
[out]返回提供的类型 [结构中TYPE_INFO信息](../../../extensibility/debugger/reference/type-info.md) 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 独立于类型的信息包括 AppDomain、模块和包含 符号的类。

## <a name="see-also"></a>请参阅
- [GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
