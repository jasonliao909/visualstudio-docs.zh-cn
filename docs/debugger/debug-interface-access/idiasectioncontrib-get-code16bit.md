---
description: 返回指示节是否包含 16 位代码的标志。
title: IDiaSectionContrib::get_code16bit | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_code16bit method
ms.assetid: 8cde8fc5-9546-4f82-b4a8-afd0d835039e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: e2617a362f49d7c360b8226dac8ba2b6cb491652
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831989"
---
# <a name="idiasectioncontribget_code16bit"></a>IDiaSectionContrib::get_code16bit
返回指示节是否包含 16 位代码的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_code16bit(
   BOOL *pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果节中的代码为 16 位，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法仅指示代码是否为 16 位。 如果代码不是 16 位，则可能是其他任何代码，例如 32 位或 64 位代码。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
