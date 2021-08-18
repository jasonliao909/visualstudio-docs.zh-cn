---
description: 切换此挂起断点的虚拟化状态。
title: IDebugPendingBreakpoint2：：虚拟化 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPendingBreakpoint2::Virtualize
helpviewer_keywords:
- Virtualize method
- IDebugPendingBreakpoint2::Virtualize method
ms.assetid: 58c8e9a5-4494-47c2-bddb-56f628da6a2d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 13add9633223fbcddbdee96db5b217ca12273f8954b0bd158e7c3429f5d47fcb
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121339068"
---
# <a name="idebugpendingbreakpoint2virtualize"></a>IDebugPendingBreakpoint2::Virtualize
切换此挂起断点的虚拟化状态。 当挂起的断点虚拟化时，调试引擎将尝试在每次将新代码加载到程序时绑定该断点。

## <a name="syntax"></a>语法

```cpp
HRESULT Virtualize(
    BOOL fVirtualize
);
```

```cpp
int Virtualize(
    int fVirtualize
);
```

## <a name="parameters"></a>参数
`fVirtualize`\
中设置为非零 `TRUE` 值 () 以虚拟化挂起断点，或设置为零， (`FALSE`) 关闭虚拟化。

## <a name="return-value"></a>返回值
如果成功， `S_OK` 则返回; 否则返回错误代码。 `E_BP_DELETED`如果已删除断点，则返回。

## <a name="remarks"></a>备注
每次加载代码时都绑定了虚拟化的断点。

## <a name="example"></a>示例
下面的示例演示如何为 `CPendingBreakpoint` 公开 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) 接口的简单对象实现此方法。

```cpp
HRESULT CPendingBreakpoint::Virtualize(BOOL fVirtualize)
{
    HRESULT hr;

    // Verify that the pending breakpoint has not been deleted. If deleted,
    // then return hr = E_BP_DELETED.
    if (m_state.state != PBPS_DELETED)
    {
        if (fVirtualize)
        {
            // Set the PBPSF_VIRTUALIZED flag in the PENDING_BP_STATE_FLAGS
            // structure.
            SetFlag(m_state.flags, PBPSF_VIRTUALIZED);
        }
        else
        {
            // Clear the PBPSF_VIRTUALIZED flag in the PENDING_BP_STATE_FLAGS
            // structure.
            ClearFlag(m_state.flags, PBPSF_VIRTUALIZED);
        }
        hr = S_OK;
    }
    else
    {
        hr = E_BP_DELETED;
    }

    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
