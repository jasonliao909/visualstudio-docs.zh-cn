---
description: 此方法在进程及其包含的所有程序上显式 ("编辑并继续") 。
title: IDebugProcess3：:D isableENC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 88be8c57bac99761ac4bcfb6d92451ba0245c483
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122071982"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
此方法在进程及其包含的所有程序上显式 ("编辑并继续") 。 自定义端口供应商应始终返回 `E_NOTIMPL` 。

## <a name="syntax"></a>语法

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>参数
`reason`\
[in] [EncUnavailableReason 枚举中的](../../../extensibility/debugger/reference/encunavailablereason.md) 值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

> [!NOTE]
> 自定义端口供应商应始终返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注
 为进程禁用"编辑并继续"后，只有重启进程才能重新启用它。

## <a name="see-also"></a>请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
