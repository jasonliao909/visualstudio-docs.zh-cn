---
description: 获取端口的名称。
title: IDebugPortRequest2：：GetPortName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 102cdc751d7c18339e02c6d3ece37f07ec65bed6
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122160044"
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

## <a name="parameters"></a>参数
`pbstrPortName`\
[out]返回端口的名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)接口通常从调试包 (客户端) 传递到服务器 (的端口) 以获取与端口的连接。 调试包和端口供应商都了解端口的可能选择。 如果简单字符串可以描述端口，则 `IDebugPortRequest2::GetPortName` 方法具有足够的信息来建立连接。 否则，客户端可以提供额外的接口，服务器可以使用 获取这些接口 `IDebugPortRequest2::QueryInterface` 。

## <a name="see-also"></a>请参阅
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
