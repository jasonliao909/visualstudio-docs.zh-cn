---
description: IDiaSymbol::findInlineFramesByVA 检索允许客户端在指定虚拟地址 (VA) 中循环访问所有内联帧的枚举。
title: IDiaSymbol::findInlineFramesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 54295d3e-bbb6-4c10-ab9d-adcfc22b1f71
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ff742a57fecf4a8443bbd1de02be17e0ff5a62d8
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831741"
---
# <a name="idiasymbolfindinlineframesbyva"></a>IDiaSymbol::findInlineFramesByVA
检索允许客户端在指定虚拟地址 (VA) 中循环访问所有内联帧的枚举。

## <a name="syntax"></a>语法

```C++
HRESULT findInlineFramesByVA ( 
   ULONGLONG         va,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>参数
 `va`

[in] 将地址指定为 VA。

 `ppResult`

[out] 保留包含已检索的帧的列表的 `IDiaEnumSymbols` 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
