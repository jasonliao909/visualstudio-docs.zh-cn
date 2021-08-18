---
description: IDebugProgramNode2：：GetProgramName 获取程序的名称。
title: IDebugProgramNode2：：GetProgramName |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetProgramName
helpviewer_keywords:
- IDebugProgramNode2::GetProgramName
ms.assetid: 510c7f5d-48ff-4d9f-ad79-fbad9f15239d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5fa8b695b624ca0edcbe64afcc0e771e51db1754
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122050567"
---
# <a name="idebugprogramnode2getprogramname"></a>IDebugProgramNode2::GetProgramName
获取程序的名称。

## <a name="syntax"></a>语法

```cpp
HRESULT GetProgramName (
    BSTR* pbstrProgramName
);
```

```csharp
int GetProgramName (
    out string pbstrProgramName
);
```

## <a name="parameters"></a>参数
`pbstrProgramName`\
[out]返回程序的名称。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
程序的名称与程序的路径不同，尽管程序的名称可能是此类路径的一部分。

## <a name="example"></a>示例
下面的示例演示如何为实现 `CProgram` [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) 接口的简单对象实现此方法。 `MakeBstr`函数将指定字符串的副本分配为 BSTR。

```cpp
HRESULT CProgram::GetProgramName(BSTR* pbstrProgramName) {
    if (!pbstrProgramName)
        return E_INVALIDARG;

    // Assign the member program name to the passed program name.
    *pbstrProgramName = MakeBstr(m_pszProgramName);
    return NOERROR;
}
```

## <a name="see-also"></a>请参阅
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
