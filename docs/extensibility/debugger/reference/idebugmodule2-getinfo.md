---
description: 获取有关此模块的信息。
title: IDebugModule2：： GetInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2::GetInfo
helpviewer_keywords:
- GetInfo method
- IDebugModule2::GetInfo method
ms.assetid: de337e66-294f-4ac9-b21e-71fac7418e36
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a31c6e40f18e3b405449179e3e5a3ea1a42acc6f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150558"
---
# <a name="idebugmodule2getinfo"></a>IDebugModule2::GetInfo
获取有关此模块的信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetInfo( 
   MODULE_INFO_FIELDS dwFields,
   MODULE_INFO*       pInfo
);
```

```cpp
int GetInfo( 
   enum_MODULE_INFO_FIELDS dwFields,
   MODULE_INFO[]           pInfo
);
```

## <a name="parameters"></a>参数
`dwFields`\
中 [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md) 枚举中的标志的组合，用于指定 `pInfo` 要填写的字段。

`pInfo`\
[in，out]用模块说明填充的 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) 结构。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)结构包含在 "**模块**" 窗口中显示的模块的名称。

## <a name="see-also"></a>另请参阅
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [MODULE_INFO_FIELDS](../../../extensibility/debugger/reference/module-info-fields.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
