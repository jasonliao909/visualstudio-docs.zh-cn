---
description: 检索调试引擎正在调试的所有程序的列表 (DE) 。
title: IDebugEngine2：： EnumPrograms |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::EnumPrograms
helpviewer_keywords:
- IDebugEngine2::EnumPrograms
ms.assetid: 56bf98eb-beec-4e5f-9ebe-46c922e54c56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f2e213ebb630cd87f9f9f336fd8f3092d24fca74
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122118965"
---
# <a name="idebugengine2enumprograms"></a>IDebugEngine2::EnumPrograms
检索调试引擎正在调试的所有程序的列表 (DE) 。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumPrograms( 
   IEnumDebugPrograms2** ppEnum
);
```

```csharp
int EnumPrograms( 
   out IEnumDebugPrograms2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄返回一个 [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md) 对象，该对象包含通过 DE 调试的所有程序的列表。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
