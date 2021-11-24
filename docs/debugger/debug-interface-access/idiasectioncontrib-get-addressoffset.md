---
description: 检索贡献地址的偏移量部分。
title: IDiaSectionContrib::get_addressOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_addressOffset method
ms.assetid: 4d569323-0e11-456d-9f92-a218bf292ecf
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9cbcc84e579ebc0152d0ca4773ed6189c9878b4a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831999"
---
# <a name="idiasectioncontribget_addressoffset"></a>IDiaSectionContrib::get_addressOffset
检索贡献地址的偏移量部分。

## <a name="syntax"></a>语法

```C++
HRESULT get_addressOffset ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回贡献地址的偏移量部分。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
