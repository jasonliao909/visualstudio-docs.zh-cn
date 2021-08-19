---
description: 为此属性创建唯一 ID，以确保它在所有其他属性中是唯一的。
title: IDebugProperty3：：CreateObjectID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::CreateObjectID
helpviewer_keywords:
- IDebugProperty3::CreateObjectID
ms.assetid: f2fa81e7-822f-456e-8729-a96a18eea771
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8072bc2d7689677b27ccc3ef63f6d9176927603c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122063975"
---
# <a name="idebugproperty3createobjectid"></a>IDebugProperty3::CreateObjectID
为此属性创建唯一 ID，以确保它在所有其他属性中是唯一的。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateObjectID(
   void
);
```

```csharp
int CreateObjectID();
```

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 当会话调试管理器希望确保此属性在所有其他属性之间唯一标识时，将调用此方法。 DE () 引擎支持此方法，除非已唯一标识了它处理的属性。 如果 DE 不支持此方法，则返回 `E_NOTIMPL` 。

 调用 DestroyObjectID 方法时，将销毁使用 创建的任何唯一 ID;这也表明对唯一标识此属性 `CreateObjectID` 的需要已结束。 [](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)

> [!NOTE]
> 没有检索此唯一 ID 的方法，因此 DE 可以在调用方法时对唯一 ID `CreateObjectID` 执行所需的任何操作。

## <a name="see-also"></a>请参阅
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [DestroyObjectID](../../../extensibility/debugger/reference/idebugproperty3-destroyobjectid.md)
