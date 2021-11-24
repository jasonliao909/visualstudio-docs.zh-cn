---
description: 检查两个符号是否相等。
title: IDiaSession::symsAreEquiv | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::symsAreEquiv method
ms.assetid: 9941d520-e203-46c0-83c3-b3a967f4fc59
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 2483a201da07fe45247e3ad0c389d969e2657772
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831856"
---
# <a name="idiasessionsymsareequiv"></a>IDiaSession::symsAreEquiv
检查两个符号是否相等。

## <a name="syntax"></a>语法

```C++
HRESULT symsAreEquiv ( 
   IDiaSymbol* symbolA,
   IDiaSymbol* symbolB
);
```

#### <a name="parameters"></a>参数
 `symbolA`

[in] 比较中使用的第一个 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

 `symbolB`

[in] 比较中使用的第二个 `IDiaSymbol` 对象。

## <a name="return-value"></a>返回值
 如果符号相等，则返回 `S_OK`；如果符号不相等，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
