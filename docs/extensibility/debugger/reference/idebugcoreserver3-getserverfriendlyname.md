---
description: 检索服务器的友好名称。
title: IDebugCoreServer3：： GetServerFriendlyName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerFriendlyName
helpviewer_keywords:
- IDebugCoreServer3::GetServerFriendlyName
ms.assetid: 7035b904-b3d7-4d9b-98d9-65714b8a8b9f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a1ccb77cca920706dc7622e98dfca62743bf3b65
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163104"
---
# <a name="idebugcoreserver3getserverfriendlyname"></a>IDebugCoreServer3::GetServerFriendlyName
检索服务器的友好名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetServerFriendlyName(
   BSTR* pbstrName
);
```

```csharp
int GetServerFriendlyName(
   out string pbstrName
);
```

## <a name="parameters"></a>参数
`pbstrName`\
弄返回服务器的友好名称。

> [!NOTE]
> 调用方负责释放字符串。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 对于用户启动的服务器，此方法返回的名称是服务器的完整名称。 对于自动启动的服务器，该名称是运行服务器的计算机的名称。

 对于面向计算机的名称，请调用 [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md) 方法。

## <a name="see-also"></a>另请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerName](../../../extensibility/debugger/reference/idebugcoreserver3-getservername.md)
