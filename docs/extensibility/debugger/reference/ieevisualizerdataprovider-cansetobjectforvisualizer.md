---
description: 此方法确定可视化工具是否可以具有其表示的数据对象进行更新。
title: IEEVisualizerDataProvider：： CanSetObjectForVisualizer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::CanSetObjectForVisualizer method
ms.assetid: 70fd3c6f-2f82-43a3-993b-c1dc8aa080bf
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0a6e01ac4b6613ae6a3eb70ba2487523f87bca6709bc474cc585cb4cfcab888f
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121291826"
---
# <a name="ieevisualizerdataprovidercansetobjectforvisualizer"></a>IEEVisualizerDataProvider::CanSetObjectForVisualizer
此方法确定可视化工具是否可以具有其表示的数据对象进行更新。

## <a name="syntax"></a>语法

```cpp
HRESULT CanSetObjectForVisualizer(
   BOOL* b
);
```

```csharp
int CanSetObjectForVisualizer(
   out int b
);
```

## <a name="parameters"></a>参数
`b`\
弄 `TRUE` 如果可更新可视化工具上的对象，则为非零 () ，如果不能，则为零 (`FALSE`) 。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 例如，如果某个对象绑定到只读内存，则该对象可能无法更改。

## <a name="see-also"></a>请参阅
- [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)
