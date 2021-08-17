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
ms.openlocfilehash: e5eceb34e8d82853289663a6b6795a266444d8635e34f33c490fe2a53307c1f2
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339055"
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
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)接口通常从调试包 (客户端) 传递给服务器 (的端口) 以获取与端口的连接。 调试包和端口供应商都了解端口的可能选择。 如果简单字符串可以描述端口，则 `IDebugPortRequest2::GetPortName` 方法具有足够的信息来建立连接。 否则，客户端可以提供额外的接口，服务器可以使用 获取这些接口 `IDebugPortRequest2::QueryInterface` 。

## <a name="see-also"></a>请参阅
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
