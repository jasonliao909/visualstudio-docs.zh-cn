---
description: 创建特定于表达式计算程序数据库的数据 (企业版) 。
title: IPropertyProxyEESide：：CreateReplacementObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d147e07fb87b016582373c46dd672f57daf1369
ms.sourcegitcommit: 68897da7d74c31ae1ebf5d47c7b5ddc9b108265b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2021
ms.locfileid: "122029237"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
创建特定于表达式计算程序数据库的数据 (企业版) 。

## <a name="syntax"></a>语法

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>参数
`dataIn`\
[in]保存 [要复制的数据的 IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 对象。

`dataOut`\
[out]返回一个新的 `IEEDataStorage` 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="remarks"></a>备注
 为此方法提供表示字节数组的 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) 对象。 此传入数据对象通常不由 企业版。 但是，此方法返回的对象始终由 企业版 实现，这使企业版在所需的任何类 `IEEDataStorage` 上实现 接口。

 请注意，传入对象提供 `IEEDataStorage` 的数据必须是传出对象中的相同 `IEEDataStorage` 数据。

## <a name="see-also"></a>请参阅
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
