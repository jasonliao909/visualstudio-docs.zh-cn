---
description: 获取与堆栈帧关联的物理地址范围的依赖于计算机的表示形式。
title: IDebugStackFrame2：： GetPhysicalStackRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
helpviewer_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
ms.assetid: 2f6992e2-ac1c-433f-83b7-a7f83a4ce63d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 41664f0e59b0eba6ae8a98599c74bd91fe26cf2a
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145919"
---
# <a name="idebugstackframe2getphysicalstackrange"></a>IDebugStackFrame2::GetPhysicalStackRange
获取与堆栈帧关联的物理地址范围的依赖于计算机的表示形式。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPhysicalStackRange ( 
   UINT64* paddrMin,
   UINT64* paddrMax
);
```

```csharp
int GetPhysicalStackRange ( 
   out ulong paddrMin,
   out ulong paddrMax
);
```

## <a name="parameters"></a>参数
`paddrMin`\
弄返回与此堆栈帧关联的最小物理地址。

`paddrMax`\
弄返回与此堆栈帧关联的最高物理地址。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的信息由会话调试管理器 (SDM) 用于对堆栈帧进行排序。

 假设调用堆栈向下减小，也就是说，新的堆栈帧添加到越来越少的内存地址。 运行时体系结构必须提供与此假设匹配的物理堆栈范围。

## <a name="see-also"></a>另请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
