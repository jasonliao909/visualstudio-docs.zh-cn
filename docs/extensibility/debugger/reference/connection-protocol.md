---
description: 指示用于在调试服务器与调试包之间通信的协议 (DE) 。
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
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a16c1f5ae1065e47b53cd3565c6fc18398bf5e05693dd43344abdc51486fd27
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121434407"
---
# <a name="connection_protocol"></a>CONNECTION_PROTOCOL
指示用于在调试服务器与调试包之间通信的协议 (DE) 。

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
未与服务器建立连接。

`CONNECTION_UNKNOWN`\
已建立连接，但类型未知。

`CONNECTION_LOCAL`\
连接到本地服务器。

`CONNECTION_PIPE`\
连接通过命名管道进行。

`CONNECTION_TCPIP`\
连接使用 TCP/IP。

`CONNECTION_HTTP`\
连接使用 HTTP (Web 服务器) 。

`CONNECTION_OTHER`\
已建立某种其他类型的连接 (当前未使用此值) 。

## <a name="remarks"></a>备注
这些值从 [GetConnectionProtocol 方法](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md) 返回。

## <a name="requirements"></a>要求
标头：msdbg.h

命名空间：Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetConnectionProtocol](../../../extensibility/debugger/reference/idebugcoreserver3-getconnectionprotocol.md)
