---
description: 此方法将当前字段枚举的副本作为单独的对象返回。
title: IEnumDebugFields：： Clone |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFields::Clone
helpviewer_keywords:
- IEnumDebugFields::Clone method
ms.assetid: 7ec265a8-696f-45ce-a2a2-0a83e96fee1b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b31ce817852f1ada7ae25326cd3b63a283b5d04b
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122095603"
---
# <a name="ienumdebugfieldsclone"></a>IEnumDebugFields::Clone
此方法将当前枚举的副本作为单独的对象返回。

## <a name="syntax"></a>语法

```cpp
HRESULT Clone(
   IEnumDebugFields** ppEnum
);
```

```csharp
int Clone(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
弄以单独的对象的形式返回此枚举的副本。

## <a name="property-valuereturn-value"></a>属性值/返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 调用此方法时，该枚举的副本具有与原始的相同的状态。 但是，副本的和原始状态是独立的，可以单独更改。

## <a name="see-also"></a>请参阅
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
