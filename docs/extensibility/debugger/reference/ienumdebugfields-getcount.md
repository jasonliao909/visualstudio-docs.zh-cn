---
title: IEnumDebugFields：： GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::GetCount
helpviewer_keywords:
- IEnumDebugFields::GetCount method
ms.assetid: 3f471b40-4db3-49f7-b504-58b2476eef74
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5725d16577b9d22d280b17cc572b7335cd2331ba
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896929"
---
# <a name="ienumdebugfieldsgetcount"></a>IEnumDebugFields::GetCount
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

## <a name="parameters"></a>parameters
`pcelt`\
弄返回枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不是习惯的 COM 枚举接口的一部分，它指定仅需实现下一个、克隆、跳过和重置。

## <a name="see-also"></a>另请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
