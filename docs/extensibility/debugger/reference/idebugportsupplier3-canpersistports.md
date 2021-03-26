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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 570409a114acbf19697b0eb3ef3e5496fdfde93a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071969"
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
