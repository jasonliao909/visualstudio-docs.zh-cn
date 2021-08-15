---
description: 返回此 对象中包含的字节数。
title: IEEDataStorage：：GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEDataStorage::GetSize
helpviewer_keywords:
- IEEDataStorage::GetSize
ms.assetid: 33d232c4-1239-4abc-922b-e1bc5b908169
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2ae0785d7c146c1fe9ca1765165540ae6243f50c5c760c77e0598b32eddd0425
ms.sourcegitcommit: c72b2f603e1eb3a4157f00926df2e263831ea472
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2021
ms.locfileid: "121321527"
---
# <a name="ieedatastoragegetsize"></a>IEEDataStorage::GetSize
返回此 对象中包含的字节数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize(
   ULONG* size
);
```

```csharp
int GetSize(
   out uint size
);
```

## <a name="parameters"></a>参数
`size`\
[out]此 对象中包含的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 使用 [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md) 方法检索实际数据字节。

## <a name="see-also"></a>另请参阅
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [GetData](../../../extensibility/debugger/reference/ieedatastorage-getdata.md)
