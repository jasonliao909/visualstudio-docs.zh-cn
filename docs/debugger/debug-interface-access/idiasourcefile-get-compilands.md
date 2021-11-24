---
description: 检索具有引用此文件的行号的编译单位的枚举器。
title: IDiaSourceFile::get_compilands | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_compilands method
ms.assetid: 57deb50a-9c22-43ea-a80c-eab205997bc4
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 88afe3bbaaa9fb7f07822ffd8690c4f040bcd896
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127831847"
---
# <a name="idiasourcefileget_compilands"></a>IDiaSourceFile::get_compilands
检索具有引用此文件的行号的编译单位的枚举器。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilands ( 
   IDiaEnumSymbols** ppRetVal
);
```

#### <a name="parameters"></a>参数
 `ppRetVal`

[out] 返回包含具有引用此文件的行号的所有编译单位的列表的 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
