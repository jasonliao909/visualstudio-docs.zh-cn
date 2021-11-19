---
description: 检索编译器的后端次要版本号。
title: IDiaSymbol：：get_backEndMinor |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_backEndMinor method
ms.assetid: 37f38d19-6685-440d-a477-7127c4f8699e
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 12629d6cbda5a2ebd49e526bab48e9eb9257a28a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832607"
---
# <a name="idiasymbolget_backendminor"></a>IDiaSymbol::get_backEndMinor
检索编译器的后端次要版本号。

## <a name="syntax"></a>语法

```C++
HRESULT get_backEndMinor ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回后端次要版本号。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK` ;否则返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示 属性不可用于 符号。

## <a name="remarks"></a>备注
 编译器通常由两个主要元素组成：前端 (分析器) （用于将源代码分析为中间形式）和后端 (代码生成器) （它将中间形式转换为程序集）。 前端的版本与后端不同并不少见。

 前端或后端版本号由三部分组成：..，其中 是主版本号，是次版本号， \<major> \<minor> \<build> \<major> \<minor> \<build> 是内部版本号。 例如，13.10.3077。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
