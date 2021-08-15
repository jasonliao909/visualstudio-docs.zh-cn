---
description: 检索此过程包含的所有程序的列表。
title: IDebugProcess2：：EnumPrograms |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumPrograms
helpviewer_keywords:
- IDebugProcess2::EnumPrograms
ms.assetid: f5b7295d-487d-464f-a4c6-d54175b07705
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63af55993f70068cd7362320eb7158c05e6b06cf283a93440d3c67aaec20baf4
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416451"
---
# <a name="idebugprocess2enumprograms"></a>IDebugProcess2::EnumPrograms
检索此过程包含的所有程序的列表。

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
[out]返回一 [个 IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md) 对象，该对象包含进程中所有程序的列表。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
