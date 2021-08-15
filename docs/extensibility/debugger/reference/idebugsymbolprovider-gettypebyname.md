---
description: 此方法将符号名称映射到符号类型。
title: IDebugSymbolProvider：：GetTypeByName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetTypeByName
helpviewer_keywords:
- IDebugSymbolProvider::GetTypeByName method
ms.assetid: b9d88d3b-8b75-484a-b9cc-dc8c0fbb4bc8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b4b27b5dc829ab68405c4cbcda6ece4a8a625fb7b9d4e2c7ffe86d9df0faf75d
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121306798"
---
# <a name="idebugsymbolprovidergettypebyname"></a>IDebugSymbolProvider::GetTypeByName
此方法将符号名称映射到符号类型。

## <a name="syntax"></a>语法

```cpp
HRESULT GetTypeByName( 
   LPCOLESTR     pszClassName,
   NAME_MATCH    nameMatch,
   IDebugField** ppField
);
```

```csharp
int GetTypeByName(
   string          pszClassName,
   NAME_MATCH      nameMatch,
   out IDebugField ppField
);
```

## <a name="parameters"></a>参数
`pszClassName`\
[in]符号名称。

`nameMatch`\
[in]选择匹配类型，例如区分大小写。 来自 NAME_MATCH [枚举的值](../../../extensibility/debugger/reference/name-match.md) 。

`ppField`\
[out]将符号类型作为 [IDebugField 对象](../../../extensibility/debugger/reference/idebugfield.md) 返回。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法是 [GetClassTypeByName 的泛型版本](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)。

## <a name="see-also"></a>另请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [NAME_MATCH](../../../extensibility/debugger/reference/name-match.md)
- [GetClassTypeByName](../../../extensibility/debugger/reference/idebugsymbolprovider-getclasstypebyname.md)
