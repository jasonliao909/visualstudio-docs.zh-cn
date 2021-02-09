---
title: IDebugProgramNode2：： GetHostMachineName_V7 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 843e5fdf91fe817681b95422474d3887de5756b0
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99898613"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> 弃用. 请勿使用。

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

## <a name="parameters"></a>parameters

`pbstrHostMachineName`\
弄返回正在运行程序的计算机的名称。

## <a name="return-value"></a>返回值

实现应总是返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注

> [!WARNING]
> 在 Visual Studio 2005 中，此方法不再使用，应始终返回 `E_NOTIMPL` 。

## <a name="see-also"></a>另请参阅

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
