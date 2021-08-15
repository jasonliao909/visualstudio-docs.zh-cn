---
description: 获取进程正在其上运行的端口。
title: IDebugProcess2：：GetPort |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetPort
helpviewer_keywords:
- IDebugProcess2::GetPort
ms.assetid: e39b6e5a-64eb-48cf-a53d-da4fdb968e2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4feae4e00fb21b1092156fcaf09d3dfab863000b23d497a1067e104e5c6dfdba
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121416282"
---
# <a name="idebugprocess2getport"></a>IDebugProcess2::GetPort
获取进程正在其上运行的端口。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPort( 
   IDebugPort2** ppPort
);
```

```csharp
int GetPort( 
   out IDebugPort2 ppPort
);
```

## <a name="parameters"></a>参数
`ppPort`\
[out]返回一 [个 IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) 对象，该对象表示启动进程的端口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
