---
description: 此方法获取此端口的 IDebugPortNotify2 接口。
title: IDebugDefaultPort2：： GetPortNotify |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetPortNotify
helpviewer_keywords:
- IDebugDefaultPort2::GetPortNotify
ms.assetid: 3ae715ee-9886-4694-a52b-59bb3b27467a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8ed43d96a7035dbd9e75a8e64a23e556997e087c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077468"
---
# <a name="idebugdefaultport2getportnotify"></a>IDebugDefaultPort2::GetPortNotify
此方法获取此端口的 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortNotify(
   IDebugPortNotify2** ppPortNotify
);
```

```csharp
int GetPortNotify(
   out IDebugPortNotify2 ppPortNotify
);
```

## <a name="parameters"></a>参数
`ppPortNotify`\
弄一个 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 通常，对 `QueryInterface` 实现 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口的对象调用方法以获取 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 接口。 但是，在某些情况下，需要在不同的对象上实现所需的接口。 此方法隐藏这些情况并 `IDebugPortNotify2` 从最适当的对象返回接口。

## <a name="see-also"></a>另请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
