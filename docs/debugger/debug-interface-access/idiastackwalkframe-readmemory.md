---
description: 从映像读取内存。
title: IDiaStackWalkFrame::readMemory | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::readMemory method
ms.assetid: 7ab0b525-a5a7-4692-acad-e8c00fa9ab9a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: de206ac94a03d6f50d301fed84067e56dbc88a30
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831803"
---
# <a name="idiastackwalkframereadmemory"></a>IDiaStackWalkFrame::readMemory
从映像读取内存。

## <a name="syntax"></a>语法

```C++
HRESULT readMemory ( 
   MemoryTypeEnum type,
   ULONGLONG va,
   DWORD     cbData,
   DWORD*    pcbData,
   BYTE      data[]
);
```

#### <a name="parameters"></a>参数
 `type`

[in] [MemoryTypeEnum Enumeration](../../debugger/debug-interface-access/memorytypeenum.md) 枚举值之一，指定了要访问的内存类型。

 `va`

[in] 要开始读取的映像中的虚拟地址位置。

 `cbData`

[in] 数据缓冲区的大小（以字节为单位）。

 `pcbData`

[out] 返回返回的字节数。 如果 `data` 为 `NULL`，则 `pcbData` 包含可用数据的总字节数。

 `data`

[out] 要使用指定位置的数据进行填充的缓冲区。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
