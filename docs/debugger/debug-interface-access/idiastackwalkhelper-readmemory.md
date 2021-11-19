---
description: 从可执行文件的内存图像中读取数据块。
title: IDiaStackWalkHelper::readMemory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::readMemory method
ms.assetid: e1eb90aa-49b7-476c-9e70-7e8f08994cbe
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 22507fb6fdc072c643675a8e99b6a578c9380118
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831768"
---
# <a name="idiastackwalkhelperreadmemory"></a>IDiaStackWalkHelper::readMemory
从可执行文件的内存图像中读取数据块。

## <a name="syntax"></a>语法

```C++
HRESULT readMemory( 
   enum MemoryTypeEnum type,
   ULONGLONG           va,
   DWORD               cbData,
   DWORD*              pcbData,
   BYTE*               pbData
);
```

#### <a name="parameters"></a>参数
 `type`

[in] [MemoryTypeEnum Enumeration](../../debugger/debug-interface-access/memorytypeenum.md) 枚举的一个值，指定要读取的内存类型。

 va

[in] 要从其开始读取的映像中的虚拟地址。

 `cbData`

[in] 数据缓冲区的大小（以字节为单位）。

 `pcbData`

[out] 返回实际读取的字节数。 如果 `pbData` 为 `NULL`，则这是可用数据的总字节数。

 `pbData`

[in, out] 使用所读取内存填充的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [MemoryTypeEnum 枚举](../../debugger/debug-interface-access/memorytypeenum.md)
