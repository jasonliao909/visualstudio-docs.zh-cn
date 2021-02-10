---
title: IDebugPortPicker：： SetSite |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugPortPicker::SetSite
ms.assetid: 7319e187-adfe-4b3f-aec9-521356fb5a8a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7c361291532a79e7e4dd466d07359f0fe9faf2be
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99958630"
---
# <a name="idebugportpickersetsite"></a>IDebugPortPicker::SetSite
设置服务提供程序。

## <a name="syntax"></a>语法

```cpp
HRESULT SetSite(
   IServiceProvider * pSP
);
```

```csharp
public int SetSite(
   IServiceProvider pSP
);
```

## <a name="parameters"></a>parameters
`pSP`\
中对服务提供程序的接口的引用。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 在调用其他任何方法之前，将调用此方法。

## <a name="see-also"></a>另请参阅
- [IDebugPortPicker](../../../extensibility/debugger/reference/idebugportpicker.md)
