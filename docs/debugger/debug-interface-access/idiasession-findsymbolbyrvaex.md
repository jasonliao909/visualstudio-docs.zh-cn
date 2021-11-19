---
description: 检索指定的符号类型，该符号类型包含或最接近 RVA 的指定 (虚拟地址) 偏移量。
title: IDiaSession：：findSymbolByRVAEx |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findSymbolByRVAEx method
ms.assetid: 61344966-fed4-4c02-9e27-20356ec2ef7c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 62a55241bf74fd57e463faabe335bee5999ad698
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831881"
---
# <a name="idiasessionfindsymbolbyrvaex"></a>IDiaSession::findSymbolByRVAEx
检索指定的符号类型，该符号类型包含或最接近 RVA 的指定 (虚拟地址) 偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT findSymbolByRVAEx ( 
   DWORD        rva,
   SymTagEnum   symtag,
   IDiaSymbol** ppSymbol,
   LONG*        displacement
);
```

#### <a name="parameters"></a>参数
 `rva`

[in]指定 RVA。

 `symtag`

[in]要找到的符号类型。 值取自 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md) 枚举。

 `ppSymbol`

[out]返回表示 [检索到的符号的 IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) 对象。

 `displacement`

[out]返回一个值，该值指定与 中指定的相对虚拟地址的偏移 `rva` 量。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回错误代码。

## <a name="example"></a>示例

```C++
IDiaSymbol* pFunc;
LONG disp = 0;
pSession->findSymbolByRVAEx( rva, SymTagFunction, &pFunc, &disp );
```

## <a name="see-also"></a>另请参阅
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
