---
description: 从对象中检索指定的字节数。
title: IEEDataStorage：：：Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f28533ad07bc7626f1576ef4422d6d20725b9450
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "102227302"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
从对象中检索指定的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetData(
   ULONG  dataSize,
   ULONG* sizeGotten,
   BYTE*  data
);
```

```csharp
int GetData(
   uint     dataSize,
   out uint sizeGotten,
   byte[]   data
);
```

## <a name="parameters"></a>参数
`dataSize`\
中要 (数组中检索的字节数 `data` 必须至少包含此数量) 。

`sizeGotten`\
弄返回实际检索到的字节数。

`data`\
[in，out]要用请求的数据填充的数组。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 此方法的建议使用是将所有数据字节检索到本地数组中，因为无法跳过检索过程中的字节数。 在这种情况下，参数 `dataSize` 应为 [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) 方法返回的值。

## <a name="see-also"></a>请参阅
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
