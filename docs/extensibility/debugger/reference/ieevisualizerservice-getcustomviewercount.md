---
description: 此方法获取此服务中可用的可视化工具类型的数目。
title: IEEVisualizerService：： GetCustomViewerCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerCount
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerCount method
ms.assetid: f7b095c2-e538-4352-8cad-d4c6d4f6bdbc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 39855c4c6e37aa5e1240d15a0ad76518d60b3af4
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103463"
---
# <a name="ieevisualizerservicegetcustomviewercount"></a>IEEVisualizerService::GetCustomViewerCount
此方法获取此服务中可用的可视化工具类型的数目。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomViewerCount(
   ULONG* pcelt
);
```

```csharp
int GetCustomViewerCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
弄返回可用可视化工具的类型数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 在它对类型可视化工具的支持中向此方法传递请求。

## <a name="see-also"></a>请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
