---
description: 创建一个枚举器，其中包含与当前符号枚举器相同的枚举状态。
title: IDiaEnumSymbols::Clone | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSymbols::Clone method
ms.assetid: 5c542025-98cf-4307-901f-b9430f780cf0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-debug
ms.workload:
- multiple
ms.openlocfilehash: 06d7e33daafc87f93637ae4acbe2049b31c71237
ms.sourcegitcommit: b12a38744db371d2894769ecf305585f9577792f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2021
ms.locfileid: "127832182"
---
# <a name="idiaenumsymbolsclone"></a>IDiaEnumSymbols::Clone
创建一个枚举器，其中包含与当前枚举器相同的枚举状态。

## <a name="syntax"></a>语法

```C++
HRESULT Clone ( 
   IDiaEnumSymbols** ppenum
);
```

#### <a name="parameters"></a>参数
 ppenum

[out] 返回包含枚举器副本的 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) 对象。 不会复制符号，只会复制枚举器。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`；否则，返回错误代码。

## <a name="see-also"></a>另请参阅
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
