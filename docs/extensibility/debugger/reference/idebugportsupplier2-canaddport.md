---
description: 验证端口供应商是否可以添加新端口。
title: IDebugPortSupplier2：： CanAddPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5c53abba81b02aa6125d4fa25ce16db85579ce5c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142656"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
验证端口供应商是否可以添加新端口。

## <a name="syntax"></a>语法

```cpp
HRESULT CanAddPort( 
   void 
);
```

```csharp
int CanAddPort();
```

## <a name="return-value"></a>返回值
 如果可以添加该端口，则返回 `S_OK` ; 否则返回， `S_FALSE` 指示没有可添加到此端口供应商的端口。

## <a name="remarks"></a>备注
 在调用 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 方法之前调用此方法，因为后者会创建端口以及添加端口，这可能是一个耗时的操作。

## <a name="see-also"></a>另请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
