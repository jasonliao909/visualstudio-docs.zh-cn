---
description: 此方法为与调试地址关联的命名空间创建一个枚举器。
title: IDebugSymbolProvider：： GetNamespacesUsedAtAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetNamespacesUsedAtAddress
helpviewer_keywords:
- IDebugSymbolProvider::GetNamespacesUsedAtAddress method
ms.assetid: 392de54b-9af0-4567-953b-1b41acd1e05c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d5c7339007f0768620eee3fe6f3dafdc7d4ab84e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168499"
---
# <a name="idebugsymbolprovidergetnamespacesusedataddress"></a>IDebugSymbolProvider::GetNamespacesUsedAtAddress
此方法为与调试地址关联的命名空间创建一个枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT GetNamespacesUsedAtAddress( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppEnum
);
```

```csharp
int GetNamespacesUsedAtAddress(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`pAddress`\
中调试地址。

`ppEnum`\
弄返回命名空间的 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 枚举器。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 可能有多个命名空间与给定的调试地址相关联，例如嵌套命名空间或多个 `using` 语句。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
