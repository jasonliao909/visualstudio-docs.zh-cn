---
description: 此方法返回请求的服务。
title: IDebugBinder3：： GetEEService |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5ecd439ba1af40a54512c3ef15efb4728c8c54a1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167667"
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
[in] `GUID` 对于供应商 (可接受) 的 null 值。

`language`\
[in] `GUID` 对于语言 (可以接受) 的 null 值。

`iid`\
[in] `IID` 要获取的服务的。

`ppService`\
弄请求的服务的接口。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 将 `IID` [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md) 接口的传递 (`IID_IEEVisualizerServiceProvider`) ，以查看类型可视化工具服务是否可用。 如果是这样，表达式计算器可以获取 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) 接口以支持类型可视化工具。 有关详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。

## <a name="see-also"></a>另请参阅
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
