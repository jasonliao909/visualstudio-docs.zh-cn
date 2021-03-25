---
description: 检索此程序已加载且正在执行的模块的列表。
title: IDebugProgram2：： EnumModules |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumModules
helpviewer_keywords:
- IDebugProgram2::EnumModules
ms.assetid: 876ac9da-3b7c-4156-b79a-8f340e9fcea6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af640cf7e76da0e6cf7bb202cda08792c783e0d5
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076025"
---
# <a name="idebugprogram2enummodules"></a>IDebugProgram2::EnumModules
检索此程序已加载且正在执行的模块的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumModules( 
   IEnumDebugModules2** ppEnum
);
```

```csharp
int EnumModules( 
   out IEnumDebugModules2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回一个包含模块列表的 [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 模块是一个 DLL 或程序集，通常在 " **模块** 调试" 窗口中列出。

## <a name="see-also"></a>另请参阅
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
