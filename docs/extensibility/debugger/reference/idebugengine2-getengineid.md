---
description: 获取调试引擎 (DE) 的 GUID。
title: IDebugEngine2：： GetEngineID |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::GetEngineID
helpviewer_keywords:
- IDebugEngine2::GetEngineID
ms.assetid: 0d5674c8-a9b9-4b72-8211-d2d68695775a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 079e3b0316bb06edb383dc74ed0e71f157d29a00
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122064326"
---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
获取调试引擎 (DE) 的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineID(
    GUID* pguidEngine
);
```

```csharp
int GetEngineID(
    out Guid pguidEngine
);
```

## <a name="parameters"></a>参数
`pguidEngine`\
弄返回已取消的的 GUID。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
典型 Guid 的一些示例包括 `guidScriptEng` 、 `guidNativeEng` 或 `guidSQLEng` 。 新的调试引擎将创建自己的用于标识的 GUID。

## <a name="example"></a>示例
下面的示例演示如何对 `CEngine` 实现 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 接口的简单对象实现此方法。

```cpp
HRESULT CEngine::GetEngineId(GUID *pguidEngine) {
    if (pguidEngine) {
        // Set pguidEngine to guidBatEng, as defined in the Batdbg.idl file.
        // Other languages would require their own guidDifferentEngine to be
        //defined in the Batdbg.idl file.
        *pguidEngine = guidBatEng;
        return NOERROR; // This is typically S_OK.
    } else {
        return E_INVALIDARG;
    }
}
```

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
