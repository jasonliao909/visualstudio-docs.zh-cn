---
description: 验证端口供应商能否添加新端口。
title: IDebugPortSupplier2：：CanAddPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::CanAddPort
helpviewer_keywords:
- IDebugPortSupplier2::CanAddPort
ms.assetid: 41f69e0a-e82c-473d-8b7a-0c40fc5730fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3203dd3ec8669a3adf37580398d1089d9a93776b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122088180"
---
# <a name="idebugportsupplier2canaddport"></a>IDebugPortSupplier2::CanAddPort
验证端口供应商能否添加新端口。

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
 如果可以添加端口，则 返回 ;否则返回 以指示无法向此端口供应商 `S_OK` `S_FALSE` 添加端口。

## <a name="remarks"></a>备注
 在调用 [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) 方法之前调用此方法，因为后一种方法会创建端口并添加它，这可能是一项耗时的操作。

## <a name="see-also"></a>请参阅
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
