---
description: 此方法获取此可视化工具表示的对象。
title: IEEVisualizerDataProvider：： GetObjectForVisualizer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::GetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::GetObjectForVisualizer method
ms.assetid: bd5376fc-13b4-40b7-9a5d-7ba8289f1b24
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aa3bc464611858345a5d1013b2d4f2ce264a789c
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122103567"
---
# <a name="ieevisualizerdataprovidergetobjectforvisualizer"></a>IEEVisualizerDataProvider::GetObjectForVisualizer
此方法获取此可视化工具表示的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetObjectForVisualizer(
   IDebugObject** ppObject
);
```

```csharp
int GetObjectForVisualizer(
   out IDebugObject ppObject
);
```

## <a name="parameters"></a>参数
`ppObject`\
弄此可视化工具表示的对象

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 `GetObjectForVisualizer` 允许返回对象的缓存版本。 如果调用方想确保对象是最新的，则会调用 [GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)。

## <a name="see-also"></a>请参阅
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
- [GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
