---
description: 指示用于调试服务器与调试包之间通信的协议 (DE) 。
title: CONNECTION_PROTOCOL |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONNECTION_PROTOCOL
helpviewer_keywords:
- CONNECTION_PROTOCOL enumeration
ms.assetid: 99df5865-8b36-486d-9f4c-d10ae2bc688a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d514b9aa0e37e90e99f21b5b4906cff9d32472db
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059491"
---
# <a name="connection_protocol"></a>CONNECTION_PROTOCOL
指示用于调试服务器与调试包之间通信的协议 (DE) 。

## <a name="syntax"></a>语法

```cpp
typedef enum tagCONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
} CONNECTION_PROTOCOL;
```

```csharp
public enum CONNECTION_PROTOCOL {
    CONNECTION_NONE    = 0,
    CONNECTION_UNKNOWN = 1,
    CONNECTION_LOCAL   = 2,
    CONNECTION_PIPE    = 3,
    CONNECTION_TCPIP   = 4,
    CONNECTION_HTTP    = 5,
    CONNECTION_OTHER   = 6
};
```

## <a name="fields"></a>字段
`CONNECTION_NONE`\
没有与服务器建立连接。

`CONNECTION_UNKNOWN`\
已建立连接，但其类型未知。

`CONNECTION_LOCAL`\
连接到本地服务器。

`CONNECTION_PIPE`\
通过命名管道进行连接。

`CONNECTION_TCPIP`\
连接使用 TCP/IP。

`CONNECTION_HTTP`\
连接通过 Web 服务器) 使用 HTTP (。

`CONNECTION_OTHER`\
已建立了某些其他类型的连接 (此值当前未) 使用。

## <a name="remarks"></a>备注
这些值从 [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md) 方法返回。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
