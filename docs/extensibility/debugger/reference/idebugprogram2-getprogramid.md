---
description: 获取此程序的 GUID。
title: IDebugProgram2：：GetProgramId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProgramId
helpviewer_keywords:
- IDebugProgram2::GetProgramId
ms.assetid: 2c31c0aa-2b71-46c7-849c-356e237d26f8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 27793da2555f8bb1f61d0a9df6b616e2a551bf4813f1d416b71d7e3cd283d858
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121276433"
---
# <a name="idebugprogram2getprogramid"></a>IDebugProgram2::GetProgramId
获取此程序的 GUID。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProgramId( 
   GUID* pguidProgramId
);
```

```csharp
int GetProgramId( 
   out Guid pguidProgramId
);
```

## <a name="parameters"></a>参数
`pguidProgramId`\
[out]返回 `GUID` 此程序的 。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调试引擎 (DE) 必须返回最初传递给 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 或 [Attach 方法的程序](../../../extensibility/debugger/reference/idebugengine2-attach.md) 标识符。 这允许跨调试器组件标识程序。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
