---
description: 返回端口供应商枚举中的元素数。
title: IEnumDebugPortSuppliers2：：GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2::GetCount
helpviewer_keywords:
- IEnumDebugPortSuppliers2::GetCount
ms.assetid: 004f78dd-87d0-41a8-bcaa-f7fadbfeb8fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 80ad8f907eac5da43e7d6ba2b460bf48cba595f0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095330"
---
# <a name="ienumdebugportsuppliers2getcount"></a>IEnumDebugPortSuppliers2::GetCount
返回 枚举中的元素数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount(
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
[out]返回 枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不是指定只需实现 、、 和 方法的 com 枚举 `Next` `Clone` `Skip` `Reset` 接口的一部分。

## <a name="see-also"></a>请参阅
- [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)
