---
description: 检索指定用户定义数据类型是否为间接虚拟基类的标志。
title: IDiaSymbol::get_indirectVirtualBaseClass | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_indirectVirtualBaseClass method
ms.assetid: 853b5c6f-e1cb-4675-ad36-9ee16e3341c3
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 06a308af7d62672e8d130ff09bae3d561047870e
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832491"
---
# <a name="idiasymbolget_indirectvirtualbaseclass"></a>IDiaSymbol::get_indirectVirtualBaseClass
检索指定用户定义数据类型是否为间接虚拟基类的标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_indirectVirtualBaseClass ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果用户定义数据类型为间接虚拟基类，则返回 `TRUE`；否则返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
