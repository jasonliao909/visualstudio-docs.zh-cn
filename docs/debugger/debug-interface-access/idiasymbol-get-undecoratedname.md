---
description: 检索 C++ 修饰名或链接名的未修饰名。
title: IDiaSymbol::get_undecoratedName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_undecoratedName method
ms.assetid: e49edf25-a51d-4787-bd5b-2bf5af827c8c
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: d68fecfd0517a44cee78dfd9ac7b0d8f88ec0eb3
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832472"
---
# <a name="idiasymbolget_undecoratedname"></a>IDiaSymbol::get_undecoratedName
检索 C++ 修饰名或链接名的未修饰名。

## <a name="syntax"></a>语法

```C++
HRESULT get_undecoratedName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回 C++ 修饰名的未修饰名。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
