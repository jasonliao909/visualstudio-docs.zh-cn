---
description: 以单独的对象的形式返回当前端口供应商枚举的副本。
title: IEnumDebugPortSuppliers2：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2::Clone
helpviewer_keywords:
- IEnumDebugPortSuppliers2::Clone
ms.assetid: 98b9914d-4f32-44da-b422-68830bce44b4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c2a91f90164f192ce646e0930360c6d5d6b6f371
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122070485"
---
# <a name="ienumdebugportsuppliers2clone"></a>IEnumDebugPortSuppliers2::Clone
以单独的对象的形式返回当前枚举的副本。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugPortSuppliers2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugPortSuppliers2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄以单独的对象的形式返回此枚举的副本。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，该枚举的副本具有与原始的相同的状态。 但是，副本的和原始状态是独立的，可以单独更改。

## <a name="see-also"></a>请参阅
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
