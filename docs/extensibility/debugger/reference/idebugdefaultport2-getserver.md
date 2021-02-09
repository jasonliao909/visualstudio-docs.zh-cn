---
title: IDebugDefaultPort2：： GetServer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e046dbad9329ae377cef6864b7bc71b2ea6a538b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894941"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
此方法获取此端口所在的服务器的接口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetServer(
   IDebugCoreServer3** ppServer
);
```

```csharp
int GetServer(
   out IDebugCoreServer3 ppServer
);
```

## <a name="parameters"></a>parameters
`ppServer`\
弄返回实现 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) 接口的对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)是由 Visual Studio 实现的，它表示端口所在的服务器。

## <a name="see-also"></a>另请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
