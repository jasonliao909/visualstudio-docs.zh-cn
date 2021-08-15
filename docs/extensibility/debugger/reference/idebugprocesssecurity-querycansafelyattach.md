---
description: 此方法允许端口供应商在用户附加到不安全进程之前显示警告。
title: IDebugProcessSecurity：： QueryCanSafelyAttach |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity::QueryCanSafelyAttach
ms.assetid: 63ec1ae8-27da-4574-aa15-1c986fe9fe58
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59d0462937ebbae2ea02fb259d7928fa2a69735b1f28859a013ac7fd60ebcbfd
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121433380"
---
# <a name="idebugprocesssecurityquerycansafelyattach"></a>IDebugProcessSecurity::QueryCanSafelyAttach
此方法允许端口供应商在用户附加到不安全进程之前显示警告。

## <a name="syntax"></a>语法

```cpp
HRESULT QueryCanSafelyAttach();
```

```csharp
int QueryCanSafelyAttach();
```

## <a name="return-value"></a>返回值
 返回值如下所示：

- `S_OK`：附加到进程是安全的，并且不会显示任何警告对话框。

- `S_FALSE`：附加可能是一个安全问题，并显示带有警告的对话框。

- `FAILURE`：附加到进程失败。

## <a name="see-also"></a>另请参阅
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
