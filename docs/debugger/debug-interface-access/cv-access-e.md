---
title: CV_access_e | Microsoft Docs
description: 获取有关 CV_access_e 枚举类型的信息，该类型指定了调试接口访问 SDK 中成员的可见性范围（访问级别）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_access_e enumeration
ms.assetid: 33c05d65-abb4-4800-a382-54a3805ea7b0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: f784380e1c96a28c200ee2f7ab70cfd21c40a343
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832400"
---
# <a name="cv_access_e"></a>CV_access_e
指定成员函数和变量的可见性范围（访问级别）。

## <a name="syntax"></a>语法

```C++
typedef enum CV_access_e {
    CV_private   = 1,
    CV_protected = 2,
    CV_public    = 3
} CV_access_e;
```

## <a name="elements"></a>元素
CV_private 成员具有专用访问权限。

CV_protected 成员具有受保护的访问权限。

CV_public 成员具有公共访问权限。

## <a name="remarks"></a>备注
这里不包括 `friend` 访问说明符，因为它通常由有权访问类的专用元素和受保护元素的非成员函数使用。 使用 [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md) 方法查找具有 `SymTagFriend` 访问权限的符号。

## <a name="requirements"></a>要求
标头：cvconst.h

## <a name="see-also"></a>另请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)
- [IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)
