---
description: 从 对象中检索指定字节数。
title: IEEDataStorage：：GetData |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetData
helpviewer_keywords:
- IEEDataStorage::GetData
ms.assetid: 4d384039-73d4-40b4-ace6-a2474c546397
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df7e30e966352a36983053d80f84f0ed4bc35f5bab577594bbefbc84c8b93879
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121415723"
---
# <a name="ieedatastoragegetdata"></a>IEEDataStorage::GetData
从 对象中检索指定字节数。

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
[in]数组中要检索 (字节数必须至少包含此字节 `data`) 。

`sizeGotten`\
[out]返回实际检索的字节数。

`data`\
[in， out]用请求的数据填充的数组。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 建议使用此方法将所有数据字节检索到本地数组中，因为无法跳过检索过程中字节。 在这种情况下，参数 `dataSize` 应为 [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md) 方法返回的值。

## <a name="see-also"></a>另请参阅
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetSize](../../../extensibility/debugger/reference/ieedatastorage-getsize.md)
