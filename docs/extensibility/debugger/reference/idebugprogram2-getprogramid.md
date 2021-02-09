---
title: IDebugProgram2：： GetProgramId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetProgramId
helpviewer_keywords:
- IDebugProgram2::GetProgramId
ms.assetid: 2c31c0aa-2b71-46c7-849c-356e237d26f8
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7723333547e0aeac7fe7a73c0dc40b36f4b6e071
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99890027"
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

## <a name="parameters"></a>parameters
`pguidProgramId`\
弄返回 `GUID` 此程序的。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调试引擎 (DE) 必须返回最初传递给 [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) 或 [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) 方法的程序标识符。 这允许跨调试器组件识别程序。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)
