---
description: 获取作为字节 blob 的属性信息。
title: IDebugCustomAttribute：： GetAttributeBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeBytes
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeBytes
ms.assetid: cf34583b-6530-4dcc-89f8-eb27e4e8d594
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bbb962a31061c24fc9b51e56b0b5c63c25f2a27a
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122127306"
---
# <a name="idebugcustomattributegetattributebytes"></a>IDebugCustomAttribute::GetAttributeBytes
获取作为字节 blob 的属性信息。

## <a name="syntax"></a>语法

```cpp
HRESULT GetAttributeBytes( 
   BYTE*  ppBlob,
   DWORD* pdwLen
);
```

```csharp
int GetAttributeBytes(
   ref byte[] ppBlob,
   ref uint   pdwLen
);
```

## <a name="parameters"></a>参数
`ppBlob`\
[in，out]用属性字节填充的数组。

`pdwLen`\
[in，out]指定要在数组中返回的最大字节数 `ppBlob` ，并返回实际写入到数组中的字节数。

## <a name="return-value"></a>返回值
 如果成功，将返回 S_OK;否则，将返回错误代码。

## <a name="remarks"></a>备注
 将 `ppBlob` 参数设置为 null 值，以返回可用的属性字节数。 然后，分配一个数组，然后将该数组传递给中的 `ppBlob` 参数。

 属性 bytes 表示自定义属性的原始数据。

## <a name="see-also"></a>请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
