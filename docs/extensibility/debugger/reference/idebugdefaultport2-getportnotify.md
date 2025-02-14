---
description: 此方法获取此端口的 IDebugPortNotify2 接口。
title: IDebugDefaultPort2：：GetPortNotify |Microsoft Docs
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32af766e0c9894ab5c1be42ef62f83d9c5d56b0a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122089324"
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
[out] [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 通常， `QueryInterface` 对实现 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 接口的对象调用 方法以获取 [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md) 接口。 但是，在某些情况下，所需接口在不同的对象上实现。 此方法隐藏这些情况，并返回 `IDebugPortNotify2` 最合适的 对象的 接口。

## <a name="see-also"></a>请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugPortNotify2](../../../extensibility/debugger/reference/idebugportnotify2.md)
