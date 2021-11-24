---
description: 返回本地符号有效的地址范围的长度。
title: IDiaSymbol::get_liveRangeLength | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_liveRangeLength
ms.assetid: ffcce3cc-085c-44eb-8145-46e3819c54f9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 54cd8fc34147fca33e8c1dcb90dce1d1649f3500
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832621"
---
# <a name="idiasymbolget_liverangelength"></a>IDiaSymbol::get_liveRangeLength
返回本地符号有效的地址范围的长度。

## <a name="syntax"></a>语法

```C++
HRESULT get_liveRangeLength ( 
   ULONGLONG* length
);
```

#### <a name="parameters"></a>参数
 `length`

[out] 返回地址范围的长度。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回错误代码。

> [!NOTE]
> 返回的错误代码表示符号没有实时范围信息。

## <a name="remarks"></a>备注

## <a name="requirements"></a>要求
 标头：Dia2.h

 库：diaguids.lib

 DLL：msdia100.dll

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
