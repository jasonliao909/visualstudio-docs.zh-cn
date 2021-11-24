---
description: 检索一个标记，该标记指示是否可以在内存中共享节。
title: IDiaSectionContrib::get_share | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_share method
ms.assetid: 05c4c896-4419-4166-8bb2-8d0934dc14b5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7866c74ec6e89883a1dfe693d033b013b46166e7
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831956"
---
# <a name="idiasectioncontribget_share"></a>IDiaSectionContrib::get_share
检索一个标记，该标记指示是否可以在内存中共享节。

## <a name="syntax"></a>语法

```C++
HRESULT get_share ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果节在内存中可共享，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果不支持此属性，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)
