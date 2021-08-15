---
description: 此方法返回字段枚举中的元素数。
title: IEnumDebugFields：：GetCount |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::GetCount
helpviewer_keywords:
- IEnumDebugFields::GetCount method
ms.assetid: 3f471b40-4db3-49f7-b504-58b2476eef74
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d1d6d2dcd626529582d0dab413fb47b4db5b789e83557fda68debf9cc0945729
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415515"
---
# <a name="ienumdebugfieldsgetcount"></a>IEnumDebugFields::GetCount
此方法返回 枚举中的元素数。

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
[out]返回 枚举中的元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 此方法不是 COM 枚举接口的一部分，该接口指定只需要实现 Next、Clone、Skip 和 Reset。

## <a name="see-also"></a>另请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
