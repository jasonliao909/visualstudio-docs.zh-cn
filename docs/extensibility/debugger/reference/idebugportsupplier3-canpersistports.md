---
description: 此方法确定端口供应商是否可以通过将端口写入) 在调试器调用之间 (来持久保存端口。
title: IDebugPortSupplier3：： CanPersistPorts |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier3::CanPersistPorts
helpviewer_keywords:
- IDebugPortSupplier3::CanPersistPorts
ms.assetid: 4127760c-e602-4e86-9232-457e382a52c7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 092f6e372d8f98e731ad90a7d261fe015d019656
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172004"
---
# <a name="idebugportsupplier3canpersistports"></a>IDebugPortSupplier3::CanPersistPorts
此方法确定端口供应商是否可以通过将端口写入) 在调试器调用之间 (来持久保存端口。

## <a name="syntax"></a>语法

```cpp
HRESULT CanPersistPorts();
```

```csharp
int CanPersistPorts();
```

## <a name="parameters"></a>参数
 无。

## <a name="return-value"></a>返回值
 `S_OK` 如果可以保留端口，则 `S_FALSE` 为，表示无法保存端口。

## <a name="remarks"></a>备注
 如果端口供应商可以持久保存端口，则应在销毁端口时执行此操作，并在再次实例化后重新加载它们。

## <a name="see-also"></a>另请参阅
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
