---
description: 检索此线程的堆栈帧列表。
title: IDebugThread2：：EnumFrameInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2::EnumFrameInfo
helpviewer_keywords:
- IDebugThread2::EnumFrameInfo
ms.assetid: 17914a71-10ea-4b6f-8982-e364f87dca53
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 81f44920bfec45f4ba6860343e1fc5f19569714a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122153129"
---
# <a name="idebugthread2enumframeinfo"></a>IDebugThread2::EnumFrameInfo
检索此线程的堆栈帧列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumFrameInfo ( 
   FRAMEINFO_FLAGS        dwFieldSpec,
   UINT                   nRadix,
   IEnumDebugFrameInfo2** ppEnum
);
```

```csharp
int EnumFrameInfo ( 
   enum_FRAMEINFO_FLAGS     dwFieldSpec,
   uint                     nRadix,
   out IEnumDebugFrameInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`dwFieldSpec`\
[in]来自 FRAMEINFO_FLAGS [标志的组合](../../../extensibility/debugger/reference/frameinfo-flags.md) ，该枚举指定要填充 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构的哪些字段。指定 `FIF_FUNCNAME_FORMAT` 标志以将函数名称格式化为单个字符串。

`nRadix`\
[in]用于设置枚举器中数值信息格式的基数。

`ppEnum`\
[out]返回一 [个 IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) 对象，该对象包含描述堆栈帧的 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) 结构的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 线程的帧按顺序排列，当前帧先枚举，最后枚举最旧帧。

## <a name="see-also"></a>请参阅
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [FRAMEINFO_FLAGS](../../../extensibility/debugger/reference/frameinfo-flags.md)
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
