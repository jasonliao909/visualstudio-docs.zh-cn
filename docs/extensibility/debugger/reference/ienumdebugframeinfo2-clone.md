---
description: 将当前 FRAMEINFO 枚举的副本作为单独的 对象返回。
title: IEnumDebugFrameInfo2：：Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2::Clone
helpviewer_keywords:
- IEnumDebugFrameInfo2::Clone
ms.assetid: cdd10489-1772-47e3-815f-a6cfd32a3c60
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 79053ad2bc01c0e3af9b78647c482509354caf866df708fcc75eb84f1b381c5e
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121338314"
---
# <a name="ienumdebugframeinfo2clone"></a>IEnumDebugFrameInfo2::Clone
将当前枚举的副本作为单独的 对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugFrameInfo2** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugFrameInfo2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]以单独的 对象返回此枚举的副本。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，枚举的副本的状态与原始 副本相同。 但是，副本的 和原始 状态是分开的，可以单独更改。

## <a name="see-also"></a>另请参阅
- [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)
