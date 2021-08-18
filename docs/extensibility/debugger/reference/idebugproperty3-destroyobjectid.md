---
description: 销毁与此属性关联的唯一 ID，指示调用方不再关注从所有其他属性中唯一标识此属性。
title: IDebugProperty3：:D estroyObjectID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9d3a8784244c35c5beb6c7711e3438d1b54386dd
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063962"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
销毁与此属性关联的唯一 ID，指示调用方不再关注从所有其他属性中唯一标识此属性。

## <a name="syntax"></a>语法

```cpp
HRESULT DestroyObjectID(
   void
);
```

```csharp
int DestroyObjectID();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 如果调试引擎不需要支持属性的唯一 ID (因为它已在内部唯一地跟踪) ，则它只需返回 `E_NOTIMPL` 此方法。

 当调用方想要确保在所有其他属性之间唯一标识此属性时，通过调用 [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) 方法创建唯一 ID。

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
