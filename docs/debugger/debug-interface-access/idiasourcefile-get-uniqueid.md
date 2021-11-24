---
description: 检索对于此图像唯一的简单整数键值。
title: IDiaSourceFile::get_uniqueId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_uniqueId method
ms.assetid: e0b8dbc0-6061-4f31-bead-2cd72be44e41
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e765d97ef7a3cde84857d91b1a02c05a122614c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831844"
---
# <a name="idiasourcefileget_uniqueid"></a>IDiaSourceFile::get_uniqueId
检索对于此图像唯一的简单整数键值。

## <a name="syntax"></a>语法

```C++
HRESULT get_uniqueId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回对于此图像唯一的简单整数键值。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 比较键（而不是字符串）可以加速行号处理。

## <a name="see-also"></a>另请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
