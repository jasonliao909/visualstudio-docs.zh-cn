---
description: 获取作为字节 Blob 的属性信息。
title: IDebugCustomAttribute：：GetAttributeBytes |Microsoft Docs
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
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "126664550"
---
# <a name="idebugcustomattributegetattributebytes"></a>IDebugCustomAttribute::GetAttributeBytes
获取作为字节 Blob 的属性信息。

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

## <a name="parameters"></a>parameters
`ppBlob`\
[in， out]用属性字节填充的数组。

`pdwLen`\
[in， out]指定在数组中返回的最大字节数，并 `ppBlob` 返回实际写入数组的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 将 `ppBlob` 参数设置为 null 值，以返回可用的属性字节数。 然后分配一个数组，然后为 参数传递该 `ppBlob` 数组。

 属性字节表示自定义属性的原始数据。

## <a name="see-also"></a>另请参阅
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
