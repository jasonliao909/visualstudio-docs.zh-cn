---
description: 此方法获取此端口所在的服务器的接口。
title: IDebugDefaultPort2：： GetServer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 877dd6fc81c4bbb865594d822da10c2749c6b493
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122079332"
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

## <a name="parameters"></a>参数
`ppServer`\
弄返回实现 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) 接口的对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)是通过 Visual Studio 实现的，它表示端口所在的服务器。

## <a name="see-also"></a>请参阅
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
