---
description: 销毁与此属性关联的唯一 ID，指示调用方不再需要将此属性与所有其他属性唯一地标识。
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 071af90af5fe22d6f6cfa662458be660edc5d39f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064821"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
销毁与此属性关联的唯一 ID，指示调用方不再需要将此属性与所有其他属性唯一地标识。

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
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 如果调试引擎不需要支持属性的唯一 Id (因为它已在内部唯一跟踪) ，则它可以只是 `E_NOTIMPL` 为此方法返回。

 如果调用方想要确保在所有其他属性中唯一标识该属性，则使用对 [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) 方法的调用来创建唯一 id。

## <a name="see-also"></a>另请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
