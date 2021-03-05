---
description: 告诉程序或程序节点哪个调试引擎 (DE) 用于调试此程序。
title: IDebugProgramEngines2：： SetEngine |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEngines2::SetEngine
helpviewer_keywords:
- IDebugProgramEngines2::SetEngine
ms.assetid: c05857ee-89cf-455e-8f1e-300cce4a2eab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17e990731059d4cee6e5f716c74edf93e13b87fb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161406"
---
# <a name="idebugprogramengines2setengine"></a>IDebugProgramEngines2::SetEngine
告诉程序或程序节点哪个调试引擎 (DE) 用于调试此程序。

## <a name="syntax"></a>语法

```cpp
HRESULT SetEngine( 
   REFGUID guidEngine
);
```

```csharp
int SetEngine( 
   ref Guid guidEngine
);
```

## <a name="parameters"></a>参数
`guidEngine`\
中DE 的 GUID。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProgramEngines2](../../../extensibility/debugger/reference/idebugprogramengines2.md)
