---
description: 返回表示托管对象的接口。
title: IDebugManagedObject：：GetManagedObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugManagedObject::GetManagedObject
helpviewer_keywords:
- IDebugManagedObject::GetManagedObject method
ms.assetid: 6abe1402-6aad-41e6-8ec1-ae12d5945992
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2e5587b3e9d03ba4e0c0f2891bbb67d856e610df
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118679"
---
# <a name="idebugmanagedobjectgetmanagedobject"></a>IDebugManagedObject::GetManagedObject
返回表示托管对象的接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetManagedObject( 
   IUnknown** ppManagedObject
);
```

```cpp
int GetManagedObject(
   out object ppManagedObject
);
```

## <a name="parameters"></a>参数
`ppManagedObject`\
[out]返回表示托管对象的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 可以从此方法返回的接口查询托管类实现的任何接口，从而允许调用其方法。

## <a name="see-also"></a>请参阅
- [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
