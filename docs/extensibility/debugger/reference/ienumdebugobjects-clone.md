---
description: 此方法将当前 IDebugObjects 枚举的副本作为单独的 对象返回。
title: IEnumDebugObjects：：Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugObjects::Clone
helpviewer_keywords:
- IEnumDebugObjects::Clone method
ms.assetid: cb7df109-d29a-4218-b900-6809091459dd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3f30c658e4e0a86cead903f511395b01d93ffc0
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095356"
---
# <a name="ienumdebugobjectsclone"></a>IEnumDebugObjects::Clone
此方法将当前枚举的副本作为单独的 对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugObjects** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugObjects ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]以单独的 对象返回此枚举的副本。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，枚举的副本的状态与原始 副本相同。 但是，副本的 和原始 状态是分开的，可以单独更改。

## <a name="see-also"></a>请参阅
- [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)
