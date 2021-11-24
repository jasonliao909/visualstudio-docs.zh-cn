---
description: 检索一个标志，该标志指示是否不应将节填充到下一个内存边界。
title: IDiaSectionContrib::get_nopad | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_nopad method
ms.assetid: f5c08603-0b3e-4e81-acf1-1b95a6a83bed
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: a6b522beb9237ca2d72b066ac16caf80827132c1
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831969"
---
# <a name="idiasectioncontribget_nopad"></a>IDiaSectionContrib::get_nopad
检索一个标志，该标志指示是否不应将节填充到下一个内存边界。

## <a name="syntax"></a>语法

```C++
HRESULT get_nopad(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果不应将节填充到下一个内存边界，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此属性通常仅在较旧的文件上可见。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
