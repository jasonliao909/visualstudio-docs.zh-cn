---
description: 此方法设置调试引擎的 (DE) GUID "。
title: IDebugEngine3：： SetEngineGuid |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetEngineGuid
helpviewer_keywords:
- IDebugEngine3::SetEngineGuid
ms.assetid: 8bdfa05d-feb7-4d98-abac-77825a04c50f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ab13c75cb0860ccf0c54d7a7fdc42d4c03e8006e
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122096346"
---
# <a name="idebugengine3setengineguid"></a>IDebugEngine3::SetEngineGuid
此方法设置调试引擎 (DE) `GUID` 。

## <a name="syntax"></a>语法

```cpp
HRESULT SetEngineGuid(
   GUID* guidEngine
);
```

```csharp
int SetEngineGuid(
   ref Guid guidEngine
);
```

## <a name="parameters"></a>参数
`guidEngine`\
[in] `GUID` 的。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
