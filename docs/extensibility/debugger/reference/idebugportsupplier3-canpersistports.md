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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66745d6e4230b89eb8a2c3b20823fa93863f66cd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050827"
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

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier3](../../../extensibility/debugger/reference/idebugportsupplier3.md)
