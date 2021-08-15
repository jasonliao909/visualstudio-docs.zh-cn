---
description: 获取运行此程序)  (DE 调试引擎的名称和 GUID。
title: IDebugProgram2：： GetEngineInfo |Microsoft Docs
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
ms.openlocfilehash: 4bea94c8cc32668d8a86a63e353e5ae9392f9ba5ed833d34a3b6afcefb1488fd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338860"
---
# <a name="idebugprogram2getengineinfo"></a>IDebugProgram2::GetEngineInfo
获取运行此程序)  (DE 调试引擎的名称和 GUID。

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
弄返回运行此程序的运行的名称。

`pguidEngine`\
弄返回运行此程序的 DE 的 GUID。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 每个 DE 都定义自己的标识的 GUID。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
