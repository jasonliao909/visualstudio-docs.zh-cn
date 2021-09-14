---
description: 获取此程序的托管进程的标题、友好名称或文件名。
title: IDebugProgramHost2：：GetHostName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 02583eca88274dc998d2fc85fce8cadc247e8e93
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126602407"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
获取此程序的托管进程的标题、友好名称或文件名。

## <a name="syntax"></a>语法

```cpp
HRESULT GetHostName( 
   DWORD dwType,
   BSTR* pbstrHostName
);
```

```csharp
int GetHostName( 
   uint dwType,
   out string pbstrHostName
);
```

## <a name="parameters"></a>parameters
`dwType`\
[in]来自 GETHOSTNAME_TYPE [枚举的值](../../../extensibility/debugger/reference/gethostname-type.md) 。

`pbstrHostName`\
[out]返回托管进程的请求名称。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 在此方法的典型实现中，将忽略 参数并返回主机 `dwType` 的友好名称。 另一种可能的实现是，将 参数传递给 `dwType` 对 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) 方法的调用，以获取名称。

## <a name="see-also"></a>另请参阅
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
