---
description: 检索一个标志，该标志指定该函数是否为引入虚拟函数。
title: IDiaSymbol::get_intro | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_intro method
ms.assetid: 101afe4a-4c57-45de-87b4-330394c6de10
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9d0db207315cf2bc8dafda9dedd533cacdef261e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832486"
---
# <a name="idiasymbolget_intro"></a>IDiaSymbol::get_intro
检索一个标志，该标志指定该函数是否为引入虚拟函数。

## <a name="syntax"></a>语法

```C++
HRESULT get_intro ( 
    BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
`pRetVal`

[out] 如果该函数为引入虚拟函数，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="example"></a>示例

```C++
class A {
    virtual int f1();
}
class B : public A {
    int f1();
}
```

`A::f1` 和 `B::f1` 均为虚拟函数，但 `A::f1` 是引入虚拟函数。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
