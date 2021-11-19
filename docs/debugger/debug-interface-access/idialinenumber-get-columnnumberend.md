---
description: 检索表达式或语句的结束位置的源列号（从1开始）。
title: IDiaLineNumber::get_columnNumberEnd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaLineNumber::get_columnNumberEnd method
ms.assetid: 02fa56c1-87b6-405a-adee-3bb6bc62de2d
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 19e3ed60a17abdb39e9027455fc4e96bcad3a32a
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832068"
---
# <a name="idialinenumberget_columnnumberend"></a>IDiaLineNumber::get_columnNumberEnd
检索表达式或语句的结束位置的源列号（从1开始）。

## <a name="syntax"></a>语法

```C++
HRESULT get_columnNumberEnd ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回表达式或语句结束的列号。 如果值为零，则不存在列结尾信息。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 `S_FALSE`如果此属性不受支持，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的列值是行中语句最后一个字符之后的位置的字节偏移量。

## <a name="see-also"></a>另请参阅
- [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)
