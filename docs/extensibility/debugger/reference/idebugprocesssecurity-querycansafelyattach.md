---
description: 此方法允许端口供应商在用户附加到不安全进程之前显示警告。
title: IDebugProcessSecurity：：QueryCanSafelyAttach |Microsoft Docs
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
ms.openlocfilehash: b9ee481bb61f0dde92b3e59cbbc728985d0074cb
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122087894"
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

- `S_OK`：附加到进程是安全的，并且未显示警告对话框。

- `S_FALSE`：附加可能是一个安全问题，并且会显示一个显示警告的对话框。

- `FAILURE`：附加到进程失败。

## <a name="see-also"></a>请参阅
- [IDebugProcessSecurity](../../../extensibility/debugger/reference/idebugprocesssecurity.md)
