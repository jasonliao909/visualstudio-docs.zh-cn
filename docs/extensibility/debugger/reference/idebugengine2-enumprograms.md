---
description: 检索由调试引擎调试的所有程序的列表，这些程序 (DE) 。
title: IDebugEngine2：：EnumPrograms |Microsoft Docs
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
ms.openlocfilehash: 8eadecaef6602d5b4c9c9f21559d26f8469cd5e38dd794b0a296fc869ebc48b5
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121261731"
---
# <a name="idebugengine2enumprograms"></a>IDebugEngine2::EnumPrograms
检索由调试引擎调试的所有程序的列表，这些程序 (DE) 。

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
[out]返回 [一个 IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md) 对象，该对象包含 DE 正在调试的所有程序的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
