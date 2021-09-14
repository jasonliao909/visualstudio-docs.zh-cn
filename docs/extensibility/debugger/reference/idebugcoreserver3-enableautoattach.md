---
description: 为指定的调试引擎启用自动附加。
title: IDebugCoreServer3：：EnableAutoAttach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4f72f0586d2d393d265aac0220b7c0c1faa64d49
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664553"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
为指定的调试引擎启用自动附加。

## <a name="syntax"></a>语法

```cpp
HRESULT EnableAutoAttach(
   GUID*     rgguidSpecificEngines,
   DWORD     celtSpecificEngines,
   LPCOLESTR pszStartPageUrl,
   BSTR*     pbstrSessionId
);
```

```csharp
int EnableAutoAttach(
   Guid[]     rgguidSpecificEngines,
   uint       celtSpecificEngines,
   string     pszStartPageUrl,
   out string pbstrSessionId
);
```

## <a name="parameters"></a>parameters
`rgguidSpecificEngines`\
[in]每个调试引擎要标记为自动附加的 GUID 数组。

`celtSpecificEngines`\
[in]中指定的引擎数 `rgguidSpecificEngines` 。

`pszStartPageUrl`\
[in]自动附加时使用的起始 URL。

`pbstrSessionID`\
[out]自动附加的会话的 ID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。 一个错误代码 `E_AUTO_ATTACH_NOT_REGISTERED` 是 ，它指示尚未注册自动附加类工厂。

## <a name="remarks"></a>备注
 启动与指定 URL 关联的程序时，将自动启动并附加指定的调试引擎。

## <a name="see-also"></a>另请参阅
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
