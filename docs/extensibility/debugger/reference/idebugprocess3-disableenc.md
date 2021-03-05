---
description: 此方法显式禁用此进程上的 "编辑并继续" (以及它包含的所有程序) 。
title: IDebugProcess3：:D isableENC |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ffedebd14f720e006c0bec2044afe80901762b52
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158483"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
此方法显式禁用此进程上的 "编辑并继续" (以及它包含的所有程序) 。 自定义端口供应商应该总是返回 `E_NOTIMPL` 。

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
中 [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) 枚举中的一个值。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

> [!NOTE]
> 自定义端口供应商应该总是返回 `E_NOTIMPL` 。

## <a name="remarks"></a>备注
 为某个进程禁用了 "编辑并继续" 后，只能通过重新启动该过程来重新启用它。

## <a name="see-also"></a>另请参阅
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
