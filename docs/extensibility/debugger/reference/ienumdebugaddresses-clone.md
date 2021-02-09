---
title: IEnumDebugAddresses：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses::Clone
helpviewer_keywords:
- IEnumDebugAddresses::Clone method
ms.assetid: 71189a00-34eb-4c71-b96e-8bd6e70c6966
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 46b7c7ba36ac6d54c10d38b17154d77be88247fe
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99912703"
---
# <a name="ienumdebugaddressesclone"></a>IEnumDebugAddresses::Clone
此方法将当前枚举的副本作为单独的对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugAddresses** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugAddresses ppEnum
);
```

## <a name="parameters"></a>parameters
`ppEnum`\
弄以单独的对象的形式返回此枚举的副本。

## <a name="property-valuereturn-value"></a>属性值/返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，该枚举的副本具有与原始的相同的状态。 但是，副本的和原始状态是独立的，可以单独更改。

## <a name="see-also"></a>另请参阅
- [IEnumDebugAddresses](../../../extensibility/debugger/reference/ienumdebugaddresses.md)
