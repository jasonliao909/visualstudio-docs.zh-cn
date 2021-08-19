---
description: 获取此程序的宿主进程的标题、友好名称或文件名。
title: IDebugProgramHost2：： GetHostName |Microsoft Docs
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
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122159602"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
获取此程序的宿主进程的标题、友好名称或文件名。

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

## <a name="parameters"></a>参数
`dwType`\
中 [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md) 枚举中的一个值。

`pbstrHostName`\
弄返回宿主进程的请求的名称。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 在此方法的典型实现中，将 `dwType` 忽略参数，并返回主机的友好名称。 另一种可能的实现方法是将 `dwType` 参数传递给 [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) 方法的调用以获取名称。

## <a name="see-also"></a>请参阅
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
