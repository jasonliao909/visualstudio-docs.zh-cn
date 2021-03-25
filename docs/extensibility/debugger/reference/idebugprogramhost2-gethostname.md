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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53b4d69be1ea24f5c240b6247539f499c9fb00fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084007"
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

## <a name="see-also"></a>另请参阅
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
