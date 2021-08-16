---
description: 返回描述对象及其在其作用域或容器中的位置的结构。
title: IDebugAddress：：GetAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f7cfdadd5a2acb31525e0329f485ac289a8ecc4c888a1ff73ca7accaea736574
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121239225"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
返回描述对象及其在其作用域或容器中的位置的结构。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAddress (
   DEBUG_ADDRESS * pAddress
);
```

```csharp
int GetAddress(
   DEBUG_ADDRESS[] pAddress
);
```

## <a name="parameters"></a>参数
`pAddress`\
[in， out]一 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 方法填充的一个结构。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 该 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 将传递给此方法，该方法随后会使用相应的信息填充该方法。 此信息的解释方式取决于返回的信息类型以及符号处理程序本身。 请参阅 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) 了解更多详细信息。

## <a name="see-also"></a>请参阅
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
