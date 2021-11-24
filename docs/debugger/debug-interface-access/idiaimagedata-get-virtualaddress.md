---
description: 检索映像的虚拟内存中的位置。
title: IDiaImageData::get_virtualAddress | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaImageData::get_virtualAddress method
ms.assetid: 67ecdc8c-d342-4d0b-b02a-c6b88e22fd02
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2f40263a7a5a512e23b668a081749d08a9657826
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832097"
---
# <a name="idiaimagedataget_virtualaddress"></a>IDiaImageData::get_virtualAddress
检索映像的虚拟内存中的位置。

## <a name="syntax"></a>语法

```C++
HRESULT get_virtualAddress ( 
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回映像的虚拟地址。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)
