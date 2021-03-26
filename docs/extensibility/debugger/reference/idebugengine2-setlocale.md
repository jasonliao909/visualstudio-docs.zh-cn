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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8f06ffce2d4fdda772cc29d09057499c32dd6f77
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087920"
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
