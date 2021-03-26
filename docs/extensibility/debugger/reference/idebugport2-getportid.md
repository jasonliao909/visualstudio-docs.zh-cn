---
description: 获取端口标识符。
title: IDebugPort2：： GetPortId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPort2::GetPortId
helpviewer_keywords:
- IDebugPort2::GetPortId
ms.assetid: 837cb924-c113-4224-aa86-3e02b33dfa70
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cdd740a2182ec321e5c23e09e389b139e09f75eb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087530"
---
# <a name="idebugport2getportid"></a>IDebugPort2::GetPortId
获取端口标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPortId( 
   GUID* pguidPort
);
```

```csharp
int GetPortId( 
   out Guid pguidPort
);
```

## <a name="parameters"></a>参数
`pguidPort`\
弄返回用于标识端口的 GUID。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
