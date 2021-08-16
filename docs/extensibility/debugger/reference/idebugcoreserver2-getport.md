---
description: 检索特定端口。
title: IDebugCoreServer2：： GetPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetPort
helpviewer_keywords:
- IDebugCoreServer2::GetPort
ms.assetid: 3f5ea4a8-6085-4600-980a-9e48f8b5be56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 61529eea2c68d5504cae9ad29ffc467d09751c9ec35db8cb3953ee4410b57ed9
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121239004"
---
# <a name="idebugcoreserver2getport"></a>IDebugCoreServer2::GetPort
检索特定端口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPort( 
   REFGUID       guidPort,
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   ref Guid        guidPort,
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>参数
`guidPort`\
中要检索的端口的 GUID。

`ppPort`\
弄返回表示所需端口的 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_PORTSUPPLIER_NO_PORT`如果没有具有给定标识符的端口，则返回。

## <a name="see-also"></a>请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
