---
description: 检索服务器的名称。
title: IDebugCoreServer3：：GetServerName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::GetServerName
helpviewer_keywords:
- IDebugCoreServer3::GetServerName
ms.assetid: 0fc3fcf5-d6a3-4a00-bf14-458b8645714e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: eddf2260b3b518fd411f649feba37d6b8e0830a1
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122111458"
---
# <a name="idebugcoreserver3getservername"></a>IDebugCoreServer3::GetServerName
检索服务器的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetServerName(
   BSTR* pbstrName
);
```

```csharp
int GetServerName(
   out string pbstrName
);
```

## <a name="parameters"></a>参数
`pbstrName`\
[out]返回服务器的名称。

> [!NOTE]
> 调用方负责释放字符串。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 对于友好的服务器名称，请调用 [GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md) 方法。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [GetServerFriendlyName](../../../extensibility/debugger/reference/idebugcoreserver3-getserverfriendlyname.md)
