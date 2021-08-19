---
description: 获取运行此程序的 DE (引擎的名称) GUID。
title: IDebugProgram2：：GetEngineInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetEngineInfo
helpviewer_keywords:
- IDebugProgram2::GetEngineInfo
ms.assetid: 3a4f2dc0-e082-4d8d-aeaf-463ab09d279b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 33d4fa887d24db3b7ec7922060b649748d9a0063
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122126578"
---
# <a name="idebugprogram2getengineinfo"></a>IDebugProgram2::GetEngineInfo
获取运行此程序的 DE (引擎的名称) GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEngineInfo( 
   BSTR* pbstrEngine,
   GUID* pguidEngine
);
```

```csharp
int GetEngineInfo( 
   out string pbstrEngine,
   out GUID   pguidEngine
);
```

## <a name="parameters"></a>参数
`pbstrEngine`\
[out]返回运行此程序的 DE 的名称。

`pguidEngine`\
[out]返回运行此程序的 DE 的 GUID。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 每个 DE 定义自己的 GUID 进行标识。

## <a name="see-also"></a>请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
