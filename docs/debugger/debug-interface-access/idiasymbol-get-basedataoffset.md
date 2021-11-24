---
description: 检索基本数据偏移量。
title: IDiaSymbol::get_baseDataOffset | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: bb2ff5ed-9293-4c37-9741-654058b571c5
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: ba716c5f597c0efd3592aaed4b0938ead6ca60fd
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832604"
---
# <a name="idiasymbolget_basedataoffset"></a>IDiaSymbol::get_baseDataOffset
检索基本数据偏移量。

## <a name="syntax"></a>语法

```C++
HRESULT get_baseDataOffset(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 指向保留基本数据偏移量的 `DWORD` 的指针。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
