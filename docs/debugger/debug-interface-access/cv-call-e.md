---
title: CV_call_e | Microsoft Docs
description: 获取有关 CV_call_e 枚举类型的消息，其指定了调试接口访问 SDK 中函数的调用约定。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 9619796bad01d9aba51026166819e5668743e02d
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832398"
---
# <a name="cv_call_e"></a>CV_call_e
指定函数的调用约定。

> [!NOTE]
> 此处仅记录最常见的枚举值。 cvconst.h 头文件中提供了完整的枚举。

## <a name="syntax"></a>语法

```C++
typedef enum CV_call_e {
    CV_CALL_NEAR_C    = 0x00,
    CV_CALL_NEAR_FAST = 0x04,
    CV_CALL_NEAR_STD  = 0x07,
    CV_CALL_NEAR_SYS  = 0x09,
    CV_CALL_THISCALL  = 0x0b,
    CV_CALL_CLRCALL   = 0x16
} CV_call_e;
```

## <a name="elements"></a>元素
CV_CALL_NEAR_C 使用近似从右到左的推送指定函数调用约定。 调用函数清除堆栈。

CV_CALL_NEAR_FAST 通过寄存器使用近似从左到右的推送指定函数调用约定。 已调用的函数使用参数字节的总和来清除堆栈。

CV_CALL_NEAR_STD 使用近似标准调用（从右到左的推送）来指定函数调用约定。

CV_CALL_NEAR_SYS 使用近似系统调用类指定函数调用约定。

CV_CALL_THISCALL 使用 `this` 调用（寄存器中传递的 `this` 指针）来指定函数调用约定。

CV_CALL_CLRCALL 指定公共语言运行时 (CLR) 使用的函数调用约定（也称为托管代码调用约定）。

## <a name="remarks"></a>备注
此枚举中的值是通过调用 [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) 方法返回的。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
