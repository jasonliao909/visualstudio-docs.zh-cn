---
description: 删除 IDE 为特定运行时体系结构或语言设置的异常列表。
title: IDebugEngine2：：RemoveAllSetExceptions |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::RemoveAllSetExceptions
helpviewer_keywords:
- IDebugEngine2::RemoveAllSetExceptions
ms.assetid: 165fbe89-802d-4d99-85ca-c10fd6cccc09
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 231bb94681311956e300c312dd971bf8d6e7d07b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122079150"
---
# <a name="idebugengine2removeallsetexceptions"></a>IDebugEngine2::RemoveAllSetExceptions
删除 IDE 为特定运行时体系结构或语言设置的异常列表。

## <a name="syntax"></a>语法

```cpp
HRESULT RemoveAllSetExceptions( 
   REFGUID guidType
);
```

```csharp
int RemoveAllSetExceptions( 
   ref Guid guidType
);
```

## <a name="parameters"></a>参数
`guidType`\
[in]语言的 GUID 或特定于运行时体系结构的调试引擎的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法删除的异常是由之前对 [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md) 方法的调用设置的。

 若要删除特定异常，请调用 [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [RemoveSetException](../../../extensibility/debugger/reference/idebugengine2-removesetexception.md)
