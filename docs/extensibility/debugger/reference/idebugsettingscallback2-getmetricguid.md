---
description: 根据给定的名称检索指标的唯一标识符。
title: IDebugSettingsCallback2：： GetMetricGuid |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugSettingsCallback2::GetMetricGuid
ms.assetid: 91092763-3362-4857-adf0-231bc1254206
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 504a47de04fde7aa0c630bf17e0a1c4ac24723ce
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168668"
---
# <a name="idebugsettingscallback2getmetricguid"></a>IDebugSettingsCallback2::GetMetricGuid
根据给定的名称检索指标的唯一标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMetricGuid(
   LPCWSTR pszType,
   REFGUID guidSection,
   LPCWSTR pszMetric,
   GUID*   pguidValue
);
```

```csharp
private int GetMetricGuid(
   string   pszType,
   ref Guid guidSection,
   string   pszMetric,
   out Guid pguidValue
);
```

## <a name="parameters"></a>参数
`pszType`\
中度量值的类型。

`guidSection`\
中部分的唯一标识符。

`pszMetric`\
中度量值的名称。

`pguidValue`\
弄返回度量值的唯一标识符。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)
