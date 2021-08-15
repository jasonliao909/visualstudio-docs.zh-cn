---
description: 此方法返回请求的服务。
title: IDebugBinder3：：GetEEService |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 241c47d6bf76324d762bb96e5ba7e154b6216fb71c16e1547037dca12b362be6
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121342604"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
此方法返回请求的服务。

## <a name="syntax"></a>语法

```cpp
HRESULT GetEEService(
   [in] GUID        vendor,
   [in] GUID        language,
   [in] GUID        iid,
   [out] IUnknown** ppService
);
```

```csharp
Int GetEEService(
   Guid       vendor,
   Guid       language,
   Guid       iid,
   out object ppService
);
```

## <a name="parameters"></a>参数
`vendor`\
[in] `GUID` 如果供应商 (为 null 值，则值为) 。

`language`\
[in] `GUID` 如果语言为 (，则 null 值是可接受的) 。

`iid`\
[in] `IID` 要获取的服务的 。

`ppService`\
[out]所请求服务的接口。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 将 `IID` [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md) 接口的 `IID_IEEVisualizerServiceProvider` () ，以查看类型可视化工具服务是否可用。 如果是这样，表达式计算程序可以获取 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) 接口以支持类型可视化工具。 有关详细信息 [，请参阅可视化和查看](../../../extensibility/debugger/visualizing-and-viewing-data.md) 数据。

## <a name="see-also"></a>另请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
