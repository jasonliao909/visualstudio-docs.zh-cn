---
description: 获取调试引擎的 GUID (DE) 。
title: IDebugEngine2：：GetEngineID |Microsoft Docs
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
ms.openlocfilehash: 4b70088fb3681eaadd793d3e0fc0b7549e71c9cdeca0faec4f5f8afd9897f2e6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121452116"
---
# <a name="idebugengine2getengineid"></a>IDebugEngine2::GetEngineID
获取调试引擎的 GUID (DE) 。

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
[out]返回 DE 的 GUID。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
典型 GUID 的一些示例包括 `guidScriptEng` `guidNativeEng` 、 或 `guidSQLEng` 。 新的调试引擎将创建自己的 GUID 进行标识。

## <a name="example"></a>示例
下面的示例演示如何为实现 `CEngine` [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 接口的简单对象实现此方法。

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

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
