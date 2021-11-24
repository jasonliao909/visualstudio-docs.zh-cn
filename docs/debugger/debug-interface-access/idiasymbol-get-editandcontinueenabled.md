---
description: 检索一个标记，该标记指示是否使用 /Z7、/Zi、/ZI（调试信息格式）编译器开关编译该模块。
title: IDiaSymbol::get_editAndContinueEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_editAndContinueEnabled method
ms.assetid: cd703c64-9ff8-4654-8493-8cde9309cb22
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 14884bee6ab80525f1e5b2ed1e26ca72658742d5
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832703"
---
# <a name="idiasymbolget_editandcontinueenabled"></a>IDiaSymbol::get_editAndContinueEnabled
检索一个标记，该标记指示是否使用 [/Z7、/Zi、/ZI（调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)编译器开关编译该模块。

## <a name="syntax"></a>语法

```C++
HRESULT get_editAndContinueEnabled ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out] 如果在编译时启用了编辑并继续，则返回 `TRUE`；否则，返回 `FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回 `S_FALSE` 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 意味着该属性对符号不可用。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [/Z7、/Zi、/ZI（调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)
