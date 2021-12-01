---
description: 指定要访问的内存的类型。
title: MemoryTypeEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- MemoryTypeEnum enumeration
ms.assetid: 8778c047-edeb-4495-8f9f-3f8bbb297099
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 5dd391950b3f5441d9f6d2b4e6030abfa5a399b2
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832808"
---
# <a name="memorytypeenum"></a>MemoryTypeEnum
指定要访问的内存的类型。

## <a name="syntax"></a>语法

```C++
enum MemoryTypeEnum {
    MemTypeCode,
    MemTypeData,
    MemTypeStack,
    MemTypeAny = -1
};
```

#### <a name="parameters"></a>参数
`MemTypeCode` 仅访问代码内存。

`MemTypeData` 访问数据或堆栈内存。

`MemTypeStack` 仅访问堆栈内存。

`MemTypeAny` 仅访问代码类型。

## <a name="remarks"></a>备注
此枚举中的值将传递到 [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md) 方法，以限制对不同类型的内存的访问。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)
