---
title: IDebugProgramNode2：：GetHostMachineName_V7 |Microsoft Docs
description: 这是一种弃用的旧方法，用于获取 2005 年 5 月之前使用的Visual Studio名称。
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 70cf6efde1b42b2cf0c381ae1c979c94c16d89bc
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122071430"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> 废弃。 请勿使用。

## <a name="syntax"></a>语法

```cpp
HRESULT GetHostMachineName_V7 (
   BSTR* pbstrHostMachineName
);
```

```csharp
int GetHostMachineName_V7 (
   out string pbstrHostMachineName
);
```

## <a name="parameters"></a>参数

`pbstrHostMachineName`\
[out]返回运行程序计算机的名称。

## <a name="return-value"></a>返回值

实现应始终返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 从 Visual Studio 2005 起，此方法不再使用，应始终返回 `E_NOTIMPL` 。

## <a name="see-also"></a>请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
