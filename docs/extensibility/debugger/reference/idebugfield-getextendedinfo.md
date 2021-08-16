---
description: 此方法获取有关字段的扩展信息。
title: IDebugField：：GetExtendedInfo |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetExtendedInfo
helpviewer_keywords:
- IDebugField::GetExtendedInfo method
ms.assetid: 46c0dd4d-4fd5-4efd-a908-71e4248e8e8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3881d9f94ca552fd675c774cdd8ec93dd2e2edfe18dca43a4a2d77b74532a245
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121451999"
---
# <a name="idebugfieldgetextendedinfo"></a>IDebugField::GetExtendedInfo
此方法获取有关字段的扩展信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetExtendedInfo( 
   REFGUID guidExtendedInfo,
   BYTE**  prgBuffer,
   DWORD*  pdwLen
);
```

```csharp
int GetExtendedInfo(
   ref Guid guidExtendedInfo,
   IntPtr[] prgBuffer,
   ref uint pdwLen
);
```

## <a name="parameters"></a>参数
`guidExtendedInfo`\
[in]选择要返回的信息。 有效值是：

|值|说明|
|-----------|-----------------|
|`guidConstantValue`|以字节序列表示的值。|
|`guidConstantType`|类型签名的类型。|

`prgBuffer`\
[out]返回扩展信息。

`pdwLen`\
[in， out]返回扩展信息的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 目前，此方法仅返回常量的类型或值。 调用方必须通过使用 C++ 代码或 C# (调用 COM) 释放 (`prgBuffer` `CoTaskMemFree` <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> 返回) 。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
