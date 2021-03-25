---
description: 获取在方法中跟随给定调试地址的调试地址。
title: IDebugSymbolProvider：： GetNextAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetNextAddress
helpviewer_keywords:
- IDebugSymbolProvider::GetNextAddress method
ms.assetid: 704eeb94-cb13-49d1-82b6-7d83ed0f19c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dc269dcfc472c2f8bb3e5a9ed9a91ecd25292870
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075570"
---
# <a name="idebugsymbolprovidergetnextaddress"></a>IDebugSymbolProvider::GetNextAddress
获取在方法中跟随给定调试地址的调试地址。

## <a name="syntax"></a>语法

```cpp
HRESULT GetNextAddress( 
   IDebugAddress*  pAddress,
   BOOL            fStatementOnly,
   IDebugAddress** ppAddress
);
```

```csharp
int GetNextAddress( 
   IDebugAddress     pAddress,
   bool              fStatementOnly,
   out IDebugAddress ppAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
中给定的调试地址。

`fStatementOnly`\
中如果为 TRUE，则将调试地址限制为单个语句。

`ppAddress`\
弄返回下一个调试地址。

## <a name="return-value"></a>返回值
 返回有效的 `HRESULT` ，通常 S_OK。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
