---
title: IDebugPortRequest2：： GetPortName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 574ea2ecb69c944bdb47ff80d7b4e26db51933da
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887154"
---
# <a name="idebugportrequest2getportname"></a>IDebugPortRequest2::GetPortName
获取端口的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortName( 
   BSTR* pbstrPortName
);
```

```csharp
int GetPortName( 
   out string pbstrPortName
);
```

## <a name="parameters"></a>parameters
`pbstrPortName`\
弄返回端口的名称。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)接口通常从调试包传递 (客户端) 到端口供应商 (服务器) 以获取到端口的连接。 调试包和端口提供程序均可识别端口的可能选项。 如果一个简单的字符串可以描述该端口，则该方法会提供 `IDebugPortRequest2::GetPortName` 足够的信息来建立连接。 否则，客户端可以提供其他接口，这些接口可由服务器使用获取 `IDebugPortRequest2::QueryInterface` 。

## <a name="see-also"></a>另请参阅
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
