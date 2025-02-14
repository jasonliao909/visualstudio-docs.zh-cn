---
description: 此方法返回此服务了解的类型可视化工具的列表。
title: IEEVisualizerService：：GetCustomViewerList |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerList
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerList method
ms.assetid: 249d26ca-914f-43af-a400-8162477223f4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3676390d81e4f95d523d6164f2664ec8337c1a32
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122125941"
---
# <a name="ieevisualizerservicegetcustomviewerlist"></a>IEEVisualizerService::GetCustomViewerList
此方法返回此服务了解的类型可视化工具的列表。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCustomViewerList(
   ULONG                celtSkip,
   ULONG                celtRequested,
   DEBUG_CUSTOM_VIEWER* rgViewers,
   ULONG*               pceltFetched
);
```

```csharp
int GetCustomViewerList(
   uint                  celtSkip,
   uint                  celtRequested,
   DEBUG_CUSTOM_VIEWER[] rgViewers,
   out uint              pceltFetched
);
```

## <a name="parameters"></a>参数
`celtSkip`\
[in]要跳过的可视化工具数。

`celRequested`\
[in]要检索的可视化工具 (指定数组大小 `rgViewers`) 。

`rgViewers`\
[in， out]要 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 的数组。

`pceltFetched`\
[out]实际检索的可视化工具数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 将请求传递给此方法，作为对类型可视化工具支持的一部分。 如果表达式评估器也为同一类型提供自定义查看器，它可以在这些自定义查看器的 [DEBUG_CUSTOM_VIEWER追加到](../../../extensibility/debugger/reference/debug-custom-viewer.md) 列表中。 确保 [GetCustomViewerCount 反映](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 这些附加查看器。

 有关 [可视化工具与查看器之间的差异的详细信息](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md) ，请参阅类型可视化工具与自定义查看器。

## <a name="see-also"></a>请参阅
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
