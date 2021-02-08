---
title: IDebugStackFrame2：： GetInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetInfo
helpviewer_keywords:
- IDebugStackFrame2::GetInfo
ms.assetid: 19c6870b-b94e-453c-bf19-82ce95b79d26
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 161796827507cf40f7ac7124ae3376d4252fb3d6
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99837523"
---
# <a name="idebugstackframe2getinfo"></a>IDebugStackFrame2::GetInfo
获取堆栈帧的说明。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo ( 
   FRAMEINFO_FLAGS dwFieldSpec,
   UINT            nRadix,
   FRAMEINFO*      pFrameInfo
);
```

```csharp
int GetInfo ( 
   enum_FRAMEINFO_FLAGS dwFieldSpec,
   uint                 nRadix,
   FRAMEINFO[]          pFrameInfo
);
```

## <a name="parameters"></a>parameters
`dwFieldSpec`\
中 [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md) 枚举中的标志的组合，用于指定 `pFrameInfo` 要填充参数的哪些字段。

`nRadix`\
中用于设置任何数字信息格式的基数。

`pFrameInfo`\
弄用堆栈帧说明填充的 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
