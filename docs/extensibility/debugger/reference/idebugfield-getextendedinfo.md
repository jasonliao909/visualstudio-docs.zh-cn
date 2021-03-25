---
description: 此方法获取有关字段的扩展信息。
title: IDebugField：： GetExtendedInfo |Microsoft Docs
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
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e17c824d2be7ff12e3e967b953e25359b650b1c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077065"
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
中选择要返回的信息。 有效值是：

|值|说明|
|-----------|-----------------|
|`guidConstantValue`|作为字节序列的值。|
|`guidConstantType`|类型签名形式的类型。|

`prgBuffer`\
弄返回扩展的信息。

`pdwLen`\
[in，out]返回扩展信息的大小（以字节为单位）。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 目前，此方法仅返回常量的类型或值。 调用方必须 `prgBuffer` 通过调用 COM 的 `CoTaskMemFree` 函数 (c + +) 或 <xref:System.Runtime.InteropServices.Marshal.FreeCoTaskMem%2A> (c # ) 来释放中返回的缓冲区。

## <a name="see-also"></a>另请参阅
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
