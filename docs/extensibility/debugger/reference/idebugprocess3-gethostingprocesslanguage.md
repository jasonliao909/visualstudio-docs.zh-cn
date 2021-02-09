---
title: IDebugProcess3：： GetHostingProcessLanguage |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::GetHostingProcessLanguage
helpviewer_keywords:
- IDebugProcess3::GetHostingProcessLanguage
ms.assetid: 52fca002-a9ef-43b1-9192-afbe7bb59ad4
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9743b03af9bf795d5f058a14e3f0d5981657e461
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915262"
---
# <a name="idebugprocess3gethostingprocesslanguage"></a>IDebugProcess3::GetHostingProcessLanguage
此方法返回一个， `GUID` 它表示由对 [SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)的调用设置的此进程的语言。

## <a name="syntax"></a>语法

```cpp
HRESULT GetHostingProcessLanguage(
   GUID* pguidLang
);
```

```csharp
int GetHostingProcessLanguage(
   out Guid pguidLang
);
```

## <a name="parameters"></a>parameters
`pguidLang`\
弄 `GUID` 此进程的语言的。 `GUID_NULL` (c + +) 或 `Guid.Empty` (c # ) 意味着未设置该语言。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)
