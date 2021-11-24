---
description: 检索各种用户定义类型 (UDT)。
title: IDiaSymbol::get_udtKind | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_udtKind method
ms.assetid: 4002f887-aea6-4475-b302-67c57079fe0a
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9083d89c7e9e981e200182f493d6745466883d91
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832474"
---
# <a name="idiasymbolget_udtkind"></a>IDiaSymbol::get_udtKind
检索各种用户定义类型 (UDT)。

## <a name="syntax"></a>语法

```C++
HRESULT get_udtKind ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回 [UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)中的一个值，该值指定 UDT 的类型：结构、类或联合。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [UdtKind 枚举](../../debugger/debug-interface-access/udtkind.md)
