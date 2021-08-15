---
description: 此方法获取服务器的计算机实用程序。
title: IDebugCoreServer2：： GetMachineUtilities_V7 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84d966c99267b60f39a8997d8a480ea028032e4abe82f16a15c111b535b278dc
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121323737"
---
# <a name="idebugcoreserver2getmachineutilities_v7"></a>IDebugCoreServer2::GetMachineUtilities_V7
此方法获取服务器的计算机实用程序。

> [!NOTE]
> 此方法已过时： [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] `E_NOTIMPL` 如果) 调用此方法，请不要使用 (总是返回。 由于历史原因，将保留它。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMachineUtilities_V7(
   IDebugMDMUtil2_V7** ppUtil
);
```

```csharp
int GetMachineUtilities_V7(
   out IDebugMDMUtil2_V7 ppUtil
);
```

## <a name="parameters"></a>参数
`ppUtil`\
弄返回 `IDebugMDMUtil2_V7` 表示计算机实用工具信息的接口。

## <a name="return-value"></a>返回值
 始终返回 `E_NOTIMPL` ，指示未实现该方法。

## <a name="remarks"></a>备注
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]`E_NOTIMPL`如果调用此方法，则始终返回。

## <a name="see-also"></a>另请参阅
- [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)
