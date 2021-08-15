---
description: 检索给定了调试地址的应用程序域标识符。
title: IDebugSymbolProviderDirect：： GetAppIDFromAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSymbolProviderDirect::GetAppIDFromAddress
- GetAppIDFromAddress
ms.assetid: d76a0f36-79c4-4c58-9db3-880b00d11610
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cc1b4db3588489fb4fc32846c655f732fb70b7b6d16d84fe4da8e35e517503c6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121402189"
---
# <a name="idebugsymbolproviderdirectgetappidfromaddress"></a>IDebugSymbolProviderDirect::GetAppIDFromAddress
检索给定了调试地址的应用程序域标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAppIDFromAddress(
   IDebugAddress* pAddress,
   DWORD*         pAppID
);
```

```csharp
int GetAppIDFromAddress(
   IDebugAddress pAddress,
   out uint      pAppID
);
```

## <a name="parameters"></a>参数
`pAddress`\
中调试地址由 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 接口表示。

`pAppID`\
弄应用程序域的标识符。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProviderDirect](../../../extensibility/debugger/reference/idebugsymbolproviderdirect.md)
