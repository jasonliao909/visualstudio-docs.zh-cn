---
description: 获取与堆栈帧关联的物理地址范围的与计算机相关的表示形式。
title: IDebugStackFrame2：：GetPhysicalStackRange |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
helpviewer_keywords:
- IDebugStackFrame2::GetPhysicalStackRange
ms.assetid: 2f6992e2-ac1c-433f-83b7-a7f83a4ce63d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f06a12af02ccf0eff164119a5a9de9058e88ec11
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029679"
---
# <a name="idebugstackframe2getphysicalstackrange"></a>IDebugStackFrame2::GetPhysicalStackRange
获取与堆栈帧关联的物理地址范围的与计算机相关的表示形式。

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
[out]返回与此堆栈帧关联的最低物理地址。

`paddrMax`\
[out]返回与此堆栈帧关联的最高物理地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的信息由会话调试管理器 (SDM) 堆栈帧进行排序。

 假定调用堆栈变小，也就是说，新的堆栈帧在内存地址越来越小时添加。 运行时体系结构必须提供符合此假设的物理堆栈范围。

## <a name="see-also"></a>请参阅
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
