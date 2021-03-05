---
description: " (DE) 设置调试引擎的区域设置。"
title: IDebugEngine2：： SetLocale |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::SetLocale
helpviewer_keywords:
- IDebugEngine2::SetLocale
ms.assetid: cd0d2cf1-2aac-43da-a830-4bb3d696c219
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 54cfd2d9d51cbad414cfb481b88f1e3277500efa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153906"
---
# <a name="idebugengine2setlocale"></a>IDebugEngine2::SetLocale
 (DE) 设置调试引擎的区域设置。

## <a name="syntax"></a>语法

```cpp
HRESULT SetLocale( 
   WORD wLangID
);
```

```csharp
int SetLocale( 
   ushort wLangID
);
```

## <a name="parameters"></a>参数
`wLangID`\
中指定语言区域设置。 例如，1033表示英语。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法由会话调试管理器 (SDM) 调用，以传播 IDE 的区域设置，以便正确本地化由 DE 返回的字符串。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
