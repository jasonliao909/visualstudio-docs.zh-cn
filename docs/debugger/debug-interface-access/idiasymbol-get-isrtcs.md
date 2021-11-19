---
description: 检索一个值，该值指示函数是否已使用堆栈帧运行时错误检查进行编译。 这是 /RTCs 标志。
title: IDiaSymbol：：get_isRTCs |Microsoft Docs
ms.date: 04/27/2021
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_isRTCs method
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 47f4ad2d6ac2265052d48af2c33471d9c03ae912
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127833010"
---
# <a name="idiasymbolget_isrtcs"></a>IDiaSymbol::get_isRTCs

返回一个值，该值指示函数是否已使用堆栈帧运行时错误检查进行编译。 这是 /RTCs 标志。

## <a name="syntax"></a>语法

```C++
HRESULT get_isRTCs ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数

 `pRetVal`

[out]指向 BOOL 的指针，该指针指定函数是否使用堆栈帧运行时错误检查进行编译。

## <a name="return-value"></a>返回值

 如果成功，则返回 `S_OK` ;否则 `S_FALSE` 返回 或错误代码。

> [!NOTE]
> 返回值 `S_FALSE` 表示属性不可用于符号。

## <a name="remarks"></a>备注

从 2019 版本 16.10 Visual Studio 2 开始支持此方法。

## <a name="requirements"></a>要求

|要求|说明|
|-----------------|-----------------|
|标头：|dia2.h|
|版本：|DIA SDK v7.0|

## <a name="see-also"></a>另请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
