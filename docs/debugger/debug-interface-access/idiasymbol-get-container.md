---
description: 此函数检索指向表示此符号的父级/容器的符号的指针。
title: IDiaSymbol::get_container | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_container method
ms.assetid: 24e832eb-80b3-484c-a41b-11477ec9de99
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 7f84b3577b407fb8e60322b2de078815e6d3af81
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832626"
---
# <a name="idiasymbolget_container"></a>IDiaSymbol::get_container
此函数检索指向表示此符号的父级/容器的符号的指针。

## <a name="syntax"></a>语法

```C++
HRESULT get_container(
   IDiaSymbol **pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 返回一个指向 `IDiaSymbol` 的指针，其中包含有关此符号容器的信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK；否则返回 S_FALSE 或错误代码。

> [!NOTE]
> 返回值 S_FALSE 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v8.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
