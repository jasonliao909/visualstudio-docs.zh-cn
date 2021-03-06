---
description: 此方法返回枚举中的 IDebugObject 元素的数目。
title: IEnumDebugObjects：： GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::GetCount
helpviewer_keywords:
- IEnumDebugObjects::GetCount method
ms.assetid: 9cbc5db4-03ae-479f-a664-13cad66ad210
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 54247fd49792b0a0ce5ed3218429b97b0ccdfcbf
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102224676"
---
# <a name="ienumdebugobjectsgetcount"></a>IEnumDebugObjects::GetCount
此方法返回枚举中的元素数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCount(
   [out] ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>参数
`pcelt`\
弄返回枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不是习惯的 COM 枚举接口的一部分，它指定仅需实现下一个、克隆、跳过和重置。

## <a name="see-also"></a>请参阅
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
